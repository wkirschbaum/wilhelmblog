---
layout: post
title: Force your mac to sleep with pmset
date: 2019-03-17 15:04 +0200
category: articles
rails: [mac]
---

I want play a video on my mac, but need it to go to sleep in 2 hours without me being around.

My first attempt was to write automation using [Hammerspoon](https://www.hammerspoon.org/), but it became more complicated
than what was necessary.

The second attempt was to use a utility on the mac called [pmset](https://en.wikipedia.org/wiki/Pmset), which simplified
my script to this:

```bash
#!/usr/bin/env bash

sleep 7200 && pmset sleepnow
```
[Also on github](https://github.com/wkirschbaum/bin/blob/master/sleepy)

Now whenever I type sleepy in my mac terminal, I am reasonably sure it will sleep in 2 hours.
