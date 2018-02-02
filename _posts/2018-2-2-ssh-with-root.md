---
layout: post
title: "ssh with root"
date:   2018-02-02
excerpt: "使用 root 账户 ssh 登录"
tags: [ssh]
comments: true
---

有时候我们需要以 **root** 身份来登录。这就需要配置一下了，因为处于安全考虑默认是不可的。我也建议在你使用完后更改回去。

编辑配置文件：

```sh
$ vi /etc/ssh/sshd_config

# 然后找到 PermitRootLogin 这一项
# 默认值一般为 PermitRootLogin prohibit-password 并且是被注释掉的
# 我们直接另起一行
PermitRootLogin yes

# 重启一下 sshd 服务
# 如果报错警告什么的用其他办法重启
# 如果怎样都不行或者嫌麻烦直接重启机器
$ systemctl restart sshd
```

