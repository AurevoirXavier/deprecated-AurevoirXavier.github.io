---
layout: post
title: "Git untracked content"
date:   2018-05-28
excerpt: "modified: xxx(modified content, untracked content)"
tags: [Git]
comments: true
---

<center><h2>modified: xxx(modified content, untracked content)</h2></center>

<!--more-->

意思就是 xxx 目录没有被跟踪。

出现这种情况一般是 git 仓库下还有另一个 git 仓库。

找到它并删除就可以正常 push 了。