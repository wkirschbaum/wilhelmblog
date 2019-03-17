---
layout: post
title: Starting a Rails Project
date: 2019-03-17 09:32 +0200
---

This is the generic steps I follow when setting up a new rails project.

### Links to the gems used in this post

- [annotate_models](https://github.com/ctran/annotate_models) Generates schema data as comments in your code files
- [rspec-rails](https://github.com/rspec/rspec-rails) A great testing library with many powerful features
- [factory_bot](https://github.com/thoughtbot/factory_bot) Generates useful factories for testing
- [pry](https://github.com/pry/pry) A powerful irb alternative
- [rubocop](https://github.com/rubocop-hq/rubocop) The ruby style guide as a gem
- [rubocop-rspec](https://github.com/rubocop-hq/rubocop-rspec) Rspec extensions for rubocop

### Generate the necessary Rails files

```bash
$ rails new awesomeproject -T --database=postgresql --skip-coffee
```

### Gems to add to help us to write code

We removed Rails testing with the `-T` flag before, so that we can add `rspec`.

```ruby
group :development, :test do
    ...
    gem 'rspec-rails'
    gem 'factory_bot'
end
```

then run

```bash
$ bundle install
```

```bash
$ rails generate rspec:install
```

### Some nice debugging tools

```ruby
group :development, :test do
    ...
    gem 'pry'
    gem 'pry-doc'
end

group :development do
    ...
    gem 'annotate'
end
```

then run

```bash
$ bundle install
```

```bash
$ rails g annotate:install
```

### For some styling confidence

```ruby
group :development do
    ...
    gem 'rubocop'
    gem 'rubocop-rspec'
end
```

then run

```bash
$ bundle install
```

and add a file `.rubocop.yml` in your project root folder

```yaml
require: rubocop-rspec
```

### Starting with a clean slate

run

```bash
$ rubocop -aR
```

and commit your changes to start developing on your awesome project


### Full initial Gemfile

```ruby
# frozen_string_literal: true

source 'https://rubygems.org'
git_source(:github) { |repo| "https://github.com/#{repo}.git" }

ruby '2.6.2'

gem 'jbuilder', '~> 2.5'
gem 'pg', '>= 0.18', '< 2.0'
gem 'puma', '~> 3.11'
gem 'rails', '~> 6.0.0.beta3'
gem 'sass-rails', '~> 5.0'
gem 'turbolinks', '~> 5'
gem 'webpacker', '>= 4.0.0.rc.3'

gem 'bootsnap', '>= 1.4.1', require: false

group :development, :test do
  gem 'byebug'
  gem 'factory_bot'
  gem 'rspec-rails', '~> 3.8'
end

group :development do
  gem 'listen', '>= 3.0.5', '< 3.2'
  gem 'web-console', '>= 3.3.0'

  gem 'spring'
  gem 'spring-watcher-listen', '~> 2.0.0'

  gem 'annotate'
  gem 'rubocop'
  gem 'rubocop-rspec'
end
```
