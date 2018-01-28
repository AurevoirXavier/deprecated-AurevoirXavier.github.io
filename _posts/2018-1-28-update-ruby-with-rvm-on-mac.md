---
layout: post
title: "Update ruby with rvm on mac"
date:   2018-01-28
excerpt: "在 mac 下通过 rvm 更新 ruby"
tags: [OS X, ruby, system]
comments: true
---

**rvm** 全名 *Ruby Version Manager (RVM)* 是国外一个开源的 **ruby** 版本管理工具，可以管理多个 **ruby** 版本并自由切换，[官网](www.rvm.io)。

安装：

```sh
$ curl -L get.rvm.io | bash -s stable
```

安装完后按照惯例查看一下版本看看是否安装成功：

```sh
$ rvm -v
```

列出当前源内的所有 **ruby** 版本：

```sh
$ rvm list known
```

安装其中一个版本（如果要最新版就不用加版本号后缀了，默认就可以）：

```sh
$ rvm install ruby
```

列出所有已安装的 **ruby**：

```sh
$ rvm list
```

调整系统默认使用版本（写本篇博客时最新版为 2.4.1，亦为上一条命令中列出的刚安装的版本）：

```sh
$ rvm alias create default 2.4.1
```

按照惯例再查看一下 **ruby** 版本（需要重启或者刷新一下终端，才能看到变动）：

```sh
$ ruby -v
```

如果要删除的话：

```sh
$ rvm remove (你想删除的版本)
```

