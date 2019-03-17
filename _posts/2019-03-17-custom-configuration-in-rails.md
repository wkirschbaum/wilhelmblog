---
layout: post
title: Custom configuration in Rails
date: 2019-03-17 13:04 +0200
category: articles
tags: [rails, programming]
---

Often I want to add more configuration to my Rails application, but I want it to be
consistent with the configuration of my `config/database.yml`.  I also don't want to
be using more gems or write a lot of code to get it working.

Let us assume we want to add a configuration file for the aws gem.  We
can start by adding a file in the config folder called aws.yml `config/aws.yml`

```yaml
common: &default
  region: <%= ENV.fetch('AWS_REGION') { 'eu-west-1' } %>
  access_key_id: <%= ENV.fetch('AWS_ACCESS_KEY_ID') { 'key' } %>
  secret_access_key: <%= ENV.fetch('AWS_SECRET_ACCESS_KEY') { 'secret' } %>

development:
  <<: *default

test:
  <<: *default

production:
  <<: *default
```

The next step would be to tell Rails about this configuration file.  You can do this
by updating the `config/application.rb` file with the following code:

```ruby
class Application < Rails::Application
    ...

    config.aws = config_for(:aws)

    ...
end
```

Now it is possible to reference your new configuration anywhere within your Rails
application.  In this case I will be adding an initializer file called
`config/initializers/aws.rb` with the following code

```ruby
Aws.config.update(
    region: Rails.configuration.aws.fetch('region')
    credentials: Aws::Credentials.new(
        Rails.configuration.aws.fetch('access_key_id'),
        Rails.configuration.aws.fetch('secret_access_key')
    ))
```

and everything should work as expected.
