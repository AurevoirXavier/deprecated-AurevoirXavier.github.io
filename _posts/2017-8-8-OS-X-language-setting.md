---
layout: post
title: "OS X Language Setting"
date:   2017-08-8
excerpt: "OS X 语言设置"
tags: [OS X]
comments: true
---

<center><h2>OSX 语言设置</h2></center>

<!--more-->

最近 OSX 迎来了几次小更新。由于地理位置在中国但平时工作环境采用英文设置，所以就导致了更新后语言不统一，部分地方英文部分地方中文。

按照以往的解决方法就是先设置为中文，重启后再设置回英文。但最近一次更新后这个方法不奏效了。

经过查阅发现一个完美解决方法，打开 `terminal` 键入以下命令后选择对应语言即可。

```sh
sudo "/System/Library/CoreServices/Language Chooser.app/Contents/MacOS/Language Chooser"
```