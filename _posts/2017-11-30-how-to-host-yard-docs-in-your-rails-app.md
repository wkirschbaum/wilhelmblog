---
layout: post
title: How to host yard docs in your rails app
date: 2017-11-30 08:15 +0200
category: articles
rails: [rails, programming]
---

For maximum convenience, but less... sound strategy, it is possible to host yard documentation in your rails app.

If you navigate to the repository, you will see there is a `RackMiddleware` class inside the [rack_adapter.rb](https://github.com/lsegal/yard/blob/master/lib/yard/server/rack_adapter.rb) file. This allows us to plug the yard docs into Rails.

```ruby
# aplication.rb
...
class YardDocsRouter < YARD::Server::Router
  def route_index; nil end
end
options = { single_library: true, router: YardDocsRouter }
libraries = {Refactor: [YARD::Server::LibraryVersion.new('MyLibrary', nil, '.yardoc')]}
config.middleware.use(YARD::Server::RackMiddleware, libraries: libraries, options: options)
...
```

We have to set the route_index to `nil`, otherwise the documentation will take over the root url because of this line in the method `def route(..)` [router.rb](https://github.com/lsegal/yard/blob/master/lib/yard/server/router.rb)
```
return route_index if path.empty? || path == docs_prefix
```
Now ensure that you have set up your libraries you want to document and then the docs will be available when you visit `/docs/MyLibrary`.

This is not pretty, but works without much effort.
