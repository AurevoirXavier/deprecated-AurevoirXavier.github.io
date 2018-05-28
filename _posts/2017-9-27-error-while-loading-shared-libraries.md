---
layout: post
title: "Error while loading shared libraries"
date:   2017-09-27
excerpt: "加载共享库出错"
tags: [Linux]
comments: true
---

<center><h2>加载共享库出错</h2></center>

<!--more-->

有时候执行某些命令的时候会出现这种情况：

```sh
./somecommand: error while loading shared libraries: xxx.so.0:cannot open shared object file: No such file or directory
```

这说明系统加载不了 **xxx.so** 这个东西。要么你系统里压根儿没有，要么就是系统不知道它的位置在哪里。

如果你不确定你的系统中有没有这个文件可以 `find` 一下：

```sh
find / -name "xxx.so"
```

如果有结果的话，记下路径然后编辑 `/etc/ld.so.conf` 这个文件：

```sh
vim /etc/ld.so.conf
```

里面一般会有一个 `include` 之类的东西，那是他从别的地方读取某些路径信息，不用管它，我们另起一行然后直接输入刚才所记下的路径。

Ps：一般而言，很多 `so` 都在 `/usr/local/lib` 和 `/usr/lib` 下，所以在 `/etc/ld.so.conf` 中加入那两个路径可以解决大部分问题。 

最后保存对 `/etc/ld.so.conf` 的修改后，要刷新一下让系统知道做了变更该去哪里寻找：

```sh
/sbin/ldconfig –v
```