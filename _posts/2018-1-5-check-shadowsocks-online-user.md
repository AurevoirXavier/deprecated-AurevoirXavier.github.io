---
layout: post
title: "Check shadowsocks online user"
date:   2018-01-05
excerpt: "查看 shadowsocks 在线用户"
tags: [Linux, netstat, shadowsocks]
comments: true
---

<center><h2>查看 shadowsocks 在线用户</h2></center>

<!--more-->

```sh
netstat -anp | grep '#' | grep '#' | grep '#' | ...
```

### 说明

每个 **#** 可以替换为你想要的限定词。比如第一个改为 **443** 就是代表查看在使用 **443** 端口的进程，因为 **ss** 一般使用 **443** 所以我就拿它举个例子，具体的每个人有可能不同。又因为 **ss** 一般是走 **tcp** 的，所以也可以替换占位符为 **tcp**。如果不想限定那么多删掉多余的 `grep` 就行了。想知道有多少用户就看有多少 **ip**，不过尽管我们通过限定关键字过滤了大部分但还是会有一些不是代表在线用户的 **ip**，这就要你自行判断了，一般通过搜索那个 **ip** 查看归属地就可以推断出是不是其他用户了。当然如果你的 **ss** 是通过分配不同账号给不同用户的话也就一目了然了，自然也不会搜到本文了 ^ ^。

更多 **netstat** 常用命令可以查看：[netstat useful command](http://uvwvu.xyz/Linux/netstat-useful-command.rs)。