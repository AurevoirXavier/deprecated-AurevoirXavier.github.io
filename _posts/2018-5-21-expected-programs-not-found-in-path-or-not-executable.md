---
layout: post
title: "Expected programs not found in PATH or not executable"
date:   2018-05-21
excerpt: "dpkg: error: expected program not found in PATH or not"
tags: [Linux]
comments: true
---

<center><h2>dpkg: error: expected program not found in PATH or not</h2></center>

<!--more-->

出现这个错误一般来说是使用 `sudo` 过程中修改了 **root** 用户的环境，大多数情况是因为改动了 `/etc/sudoers` 这个文件的这一行：

```sh
Defaults env_reset -> Defaults !env_reset
```

上面这个变动代表使用 `sudo` 命令时候继承当前用户的环境变量，问题解决方法就是改回去。另外我建议直接添加环境变量到该文件中:

```sh
Defaults secure_path="/xxx"
```

这样就不会破坏 **root** 用户原有的环境变量。