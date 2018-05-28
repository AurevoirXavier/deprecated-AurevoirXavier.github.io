---
layout: post
title: "x file(s) could not be loaded into the NERD tree"
date:   2018-02-26
excerpt: "x file(s) could not be loaded into the NERD tree"
tags: [nerdtree, vim]
comments: true
---

<center><h2>x file(s) could not be loaded into the NERD tree</h2></center>

<!--more-->

一般是所有者的问题，打开问题所在路径：

```sh
# 列出所有文件及其所有者，我的 l 命令是 oh-my-zsh 中的，此处替换为你们使用的。
$ l

# 接下来你有 2 种选择

# 1.将所有文件改为当前用户所拥有
$ chown $(whoami) *

# 2.删除不是当前用户的文件（记得备份）
```