---
layout: post
title: "ruby: bad interpreter"
date:   2018-01-28
excerpt: "ruby: bad interpreter"
tags: [Ruby]
comments: true
---

<center><h2>ruby: bad interpreter</h2></center>

<!--more-->

由于删除重建用户目录丢失了一些东西。当我在终端运行 `bundle` 的时候，出了一个错误：

```sh
zsh: /usr/local/bin/bundle: /usr/local/bin/ruby: bad interpreter: No such file or directory.
```

**bundle** 的可执行文件由 *bundler gem* 提供。如果正在使用 **rvm**，那么看看 `/usr/local/bin/bundle` 中的哪个包有问题，因为使用 **rvm** 意味着像 **bundler** 那样的 **gem** 安装在你的用户目录下，通常在 `~/.rvm/gems/....`。问题一目了然，目录下的 `.rvm/` 不在了。那么重新安装 **rvm** 并用其安装 **ruby** 即可（方法可以参见这一篇[文章](https://uvwvu.xyz/OS-X/update-Ruby-with-rvm-on-mac.rs)）。

安装完后（如果你不是使用 **rvm** 直接从修复 **bundler** 步骤开始）：

```sh
# 一开始出现的错误
$ bundle install
zsh: /usr/local/bin/bundle: bad interpreter: /System/Library/Frameworks/Ruby.framework/Versions/2.0/usr/bin: no such file or directory
# 看起来是路径出了问题，gem 并不在那里

# 现在修复 bundler
$ gem uninstall bundler
$ gem install bundler

# 应该可以工作了，试试看
$ bundle install
Fetching gem metadata from http://rubygems.org/..........
```