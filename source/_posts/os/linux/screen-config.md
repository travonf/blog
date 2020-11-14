---
title: screen配置
date: 2010-01-01 08:00:00
updated: 2010-01-01 08:00:00
tags: ["linux", "screen"]
categories: ["OS", "Linux"]
---

```shell
# cat ~/.screenrc
hardstatus on
hardstatus alwayslastline
hardstatus string "%{.bW}%-w%{.rW}%n %t%{-}%+w %=%{..G} %H %{..Y} %m/%d %C%a "
startup_message off
termcapinfo xterm* ti@:te@
```
