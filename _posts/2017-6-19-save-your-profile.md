---
layout: post
title: "Save your profile"
date:   2017-06-19
excerpt: "Profile 改错了怎么办"
tags: [linux, macOS, Unix]
comments: true
---

 

在修改 **profile** 的时候，不小心改错了，除了 `cd` 以外的命令基本都不能用了，这时该怎么办 ？

连 `vi` 都不能用了，如何拯救你的 **profile**？

打开你的 **terminal** 输入：

```shell
 export PATH=/usr/bin:/usr/sbin:/bin:/sbin:/usr/X11R6/bin
```

这时再使用 `vi` 或者 `nano` 之类的工具，将 **profile** 改回来吧。 

为什么有这种操作？

原因就是 **shell** 命令基本都在 `/usr/bin`，`/usr/sbin`，`/bin`，`/sbin`，`/usr/X11R6/bin` 中有定义。所以，只要把这些命令从中取出来就可以了。