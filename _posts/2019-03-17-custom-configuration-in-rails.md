---
layout: post
title: Custom configuration in Rails
date: 2019-03-17 13:04 +0200
category: articles
tags: rails, programming
---

Often I want to add more configuration to my Rails application, but I want it to be
consistent with the configuration of my `config/database.yml`.  I also don't want to
be using more gems or write a lot of code to get it working.

Let us assume we want to add a configuration file for the aws gem to set the region.  We
can start by adding a file in the config folder called aws.yml `config/aws.yml`

```yaml
common: &default
  aws_region: 'eu-west-1'

development:
  <<: *default

test:
  <<: *default

production:
  <<: *default
  aws_region: <%= ENV.fetch('AWS_REGION') { 'eu-west-1' } %>
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

Not it is possible to reference your new configuration anywhere within your Rails
application.  In this case I will be adding an initializer file called
`config/initializers/aws.rb` with the following code

```ruby
Aws.config.update(region: Rails.configuration.aws.fetch('aws_region'))
```

and everything should work as expected.


As a note:

Using `fetch` is important here, because if the configuration is not present, we want
to be warned on application startup, not later as a surprise.
