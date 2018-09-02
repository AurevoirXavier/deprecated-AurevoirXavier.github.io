---
layout: post
title: "allow remote connection to PostgreSQL"
date:   2018-03-16
excerpt: "允许远程连接 PostgreSQL 数据库"
tags: [Linux, PostgreSQL]
comments: true
---

<center><h2>允许远程连接 PostgreSQL 数据库</h2></center>

<!--more-->

要允许远程登录一共要修改两个文件分别是 `/var/lib/pgsql/data/pg_hba.conf` 和 `/var/lib/pgsql/data/postgresql.conf`。

那么先说说第一个怎么改：

```sh
# 旧版本的 conf 文件在 /var/lib/pgsql/data/ 下
$ sudo vi /var/lib/postgres/data/pg_hba.conf

# 下面是文件里面默认允许的 ip 范围：
# IPv4 local connections:
host    all         all         127.0.0.1/32          trust
# IPv6 local connections:
host    all         all         ::1/128               trust

# 为了方便我直接改成了全部都允许：
# IPv4 local connections:
host    all         all         all                   trust
# IPv6 local connections:
host    all         all         all                   trust
# 不想全部允许的话改变加一条 ip，自行替换下面的例子：
host    all         all         [ip]/[subnet mask]    trust
```

**注意：如果 method 为 trust 说明无需验证密码，如果远程登录要验证密码改为 password，当然你可以保持 turst 然后通过限定前面 ip 范围同样起到一个验证效果。[更多配置参考](https://www.postgresql.org/docs/10/static/auth-methods.html)**

然后另一个文件这么改：

```sh
# 旧版本的 conf 文件在 /var/lib/pgsql/data/ 下
$ sudo vi /var/lib/postgres/data/postgresql.conf

# 下面是文件里面默认监听的 ip：
listen_addresses = 'localhost'

# 为了方便同样我也把它改成了监听所有，不想全部的话填写你的 ip 就可以了：
listen_addresses = '*'
```

然后重启数据库服务，即可远程连接上去啦。

---

后续补充：

今天我在 *debian* 服务器上安装了 9.6 版本因此配置有些许变化。两个文件的位置移到了 `/etc/postgresql/9.6/main/` 下面。