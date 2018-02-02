---
layout: post
title: "Raspberry PI 3 install ArchLinux"
date:   2018-02-02
excerpt: "Raspberry PI 3 安装 ArchLinux"
tags: [archlinux, raspberry pi, ]
comments: true
---

Grammar：

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