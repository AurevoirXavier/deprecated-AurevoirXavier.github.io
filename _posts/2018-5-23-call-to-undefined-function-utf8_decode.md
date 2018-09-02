---
layout: post
title: "call to undefined function utf8_decode()"
date:   2018-05-23
excerpt: "Call to undefined function utf8_decode()"
tags: [php]
comments: true
---

<center><h2>Call to undefined function utf8_decode()</h2></center>

<!--more-->

这个错误是由于缺少函数 `utf8_decode()`，原因是该函数在模块 **php7.0-xml** 中，因此只要安装该模块即可解决问题。

`apt-get install php7.0-xml`