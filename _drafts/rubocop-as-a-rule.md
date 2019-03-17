---
layout: post
title: Rubocop as a Rule
category: articles
tags: ruby
---

If you have not heard of [Rubocop](https://github.com/rubocop-hq/rubocop), check it out.  It is
a convenient gem for flagging potential code smells or bad formatting.

In my recent years of working on Rails projects in different teams, I have seen two extremes when it
comes to using Rubocop.

### 1) Infinitely Relaxing Rubocop rules

Rubocop can be configured to ignore certain warnings, or to relax certain criteria for warnings.  It
is possible to set the maximum line count per method to 100 if you wish, for example.

```yaml
Metrics/MethodLength:
  Max: 25
```

The problem is that it only expands, it never contracts


### 2) Aiming for the perfect code

Refactoring to satisfy Rubocop mechanically, which results in splitting the context with the wrong
levels of abstractions.


### More habits I have seen
Littering the code with Rubocop exceptions
