---
layout: post
title: "ssh without password"
date:   2018-02-02
excerpt: "ssh 免密登录"
tags: [Note]
comments: true
---

<center><h2>ssh 免密登录</h2></center>

<!--more-->

Command：

```sh
$ ssh-copy-id [-i [identity_file]] [user@]machine
```

Option：

```sh
-i：指定公钥文件
```

Example：

把本地的 *ssh 公钥* 文件安装到远程主机对应的账户下：

```sh
$ ssh-copy-id user@server
$ ssh-copy-id -i ~/.ssh/id_rsa.pub user@server
```