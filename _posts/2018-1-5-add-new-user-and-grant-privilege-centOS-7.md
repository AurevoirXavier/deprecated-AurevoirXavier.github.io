---
layout: post
title: "Add new user and grant privilege in CentOS 7"
date:   2018-01-05
excerpt: "CentOS 7中添加一个新用户并授权"
tags: [gfw, linux, netstat, shadowsocks]
comments: true
---

<center><h2>CentOS 7中添加一个新用户并授权</h2></center>

<!--more-->

**创建新用户**

创建一个用户名为：ax

```sh
$ adduser ax
```

为这个用户初始化密码，*linux* 会判断密码复杂度，不过可以强行忽略：

```sh
$ passwd ax
```

**授权**

个人用户的权限只可以在本 `/home` 下有完整权限，其他目录要看别人授权。而经常需要 **root** 用户的权限，这时候 `sudo` 可以化身为 **root** 来操作。我记得我曾经 `sudo` 创建了文件，然后发现自己并没有读写权限，因为查看权限是 **root** 创建的。新创建的用户并不能直接使用 `sudo` 命令，需要添加授权。

`sudo` 命令的授权管理是在 **sudoers** 文件里的。可以看看 `sudoers`：

```sh
$ sudoers
```

如果提示未找到命令，我们使用 `whereis`：

```sh
$ whereis sudoers
sudoers: /etc/sudoers /etc/sudoers.d /usr/libexec/sudoers.so /usr/share/man/man5/sudoers.5.gz
```

找到这个文件位置之后再查看权限：

```sh
$ ls -l /etc/sudoers
```

是的，只有只读的权限，如果想要修改的话，需要先添加w权限：

```sh
$ chmod -v u+w /etc/sudoers
```

然后就可以添加内容了，在下面的一行下追加新增的用户：

```sh
$ vim /etc/sudoers
```

以下为 **sudoers** 内容：

```sh
## Allow root to run any commands anywher  
root    ALL=(ALL)       ALL  
ax	    ALL=(ALL)       ALL  #这个是新增的用户
```

`:wq` 保存退出，这时候要记得将写权限收回：

```sh
$ chmod -v u-w /etc/sudoers
mode of "/etc/sudoers" changed from 0640 (rw-r-----) to 0440 (r--r-----)
```

这时候使用新用户登录，使用 `sudo`：

```sh
$ sudo cat /etc/passwd
[sudo] password for ax: 

We trust you have received the usual lecture from the local System
Administrator. It usually boils down to these three things:

    #1) Respect the privacy of others.
    #2) Think before you type.
    #3) With great power comes great responsibility.
```

需要输入密码才可以下一步。如果不想需要输入密码怎么办，将最后一个 `ALL` 修改成 `NOPASSWD: ALL`。