---
layout: post
title: "Change username and hostname on Archlinux"
date:   2018-02-02
excerpt: "更改 Archlinux 中的用户名和主机名"
tags: [Archlinux, raspberry pi]
comments: true
---

一般来说这些是不用改的，而且改了会有一些配置对不上路径。不过我是给 *raspberry pi* 装了一个 *Archlinux ARM*，里面有个默认用户 `alarm` 并且主机名是 `alarmpi`。

那么先来说如何更改用户名吧（[参考资料](https://wiki.archlinux.org/index.php/Users_and_groups#Change_a_user.27s_login_name_or_home_directory)）：

```sh
$ usermod -d /my/new/home -m username
```

1.  `/my/new/home` 这个是你的新的用户目录比如我就改成 `/home/aurevoirxavier`。

2.  `username` 就是要更改的用户名。（注意不是你想改的而是现有的）这里我填写 `alarm`。

    **注意：不要登录你要修改的用户来修改！！。**

接着更改主机名（[参考资料](https://wiki.archlinux.org/index.php/Network_configuration#Set_the_hostname)）：

```sh
$ hostnamectl set-hostname myhostname
```

1.  只需要把 `myhostname` 替换成你想要的即可，我这里替换为 `aurevoirxavier`。


