---
layout: post
title: Fearing the Rails generator
date: 2019-03-17 12:36 +0200
category: articles
tags: [rails, programming]
---

Rails generators works really well and saves a minute here and there if you remember how to use them.  You can generate a controller
with a view pretty quickly with something like `rails g controller home index`. This will generate a new controller called HomeController
with an action called index. As a additional benefit it will generate a sample index page for you... and a spec file... and css file...
and a coffee file... and a helper file.

```bash
      create  app/controllers/home_controller.rb
       route  get 'home/index'
      invoke  erb
      create    app/views/home
      create    app/views/home/index.html.erb
      invoke  rspec
      create    spec/controllers/home_controller_spec.rb
      create    spec/views/home
      create    spec/views/home/index.html.erb_spec.rb
      invoke  helper
      create    app/helpers/home_helper.rb
      invoke    rspec
      create      spec/helpers/home_helper_spec.rb
      invoke  assets
      invoke    coffee
      create      app/assets/javascripts/home.coffee
      invoke    scss
      create      app/assets/stylesheets/home.scss
```

The view and the spec file is nice to have, but I have never used the helper, coffee or css file and end up deleting them.  The critique I have
been getting is that if I am going to delete more files than what I use, why not just create the files I use without using the generator? Sure, but I
am lazy and deleting code is more satisfying than adding code.

Another option is to configure rails to not generate the files you don't need.  This is pretty simple: add this configuration to your `config/application.rb`

```ruby
# config/applicaion.rb
    ...

    config.generators do |g|
      g.helper false
      g.assets false
      g.skip_routes true
    end

    ...
```

then run the command again

`rails g controller home index`

```bash
      create  app/controllers/home_controller.rb
      invoke  erb
      create    app/views/home
      create    app/views/home/index.html.erb
      invoke  rspec
      create    spec/controllers/home_controller_spec.rb
      create    spec/views/home
      create    spec/views/home/index.html.erb_spec.rb
```

and you only get what you need, and not all the extras.
