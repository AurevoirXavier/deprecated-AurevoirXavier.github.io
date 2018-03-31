---
layout: post
title: "Allow remote connection to PostgreSQL"
date:   2018-03-16
excerpt: "远程连接 PostgreSQL 数据库"
tags: [PostgreSQL]
comments: true
---

要允许远程登录一共要修改两个文件分别是 `/var/lib/pgsql/data/pg_hba.conf` 和 `/var/lib/pgsql/data/postgresql.conf`。

那么先说说第一个怎么改：

```sh
# 旧版本的 conf 文件在 /var/lib/pgsql/data/ 下
$ sudo vi /var/lib/postgres/data/pg_hba.conf

# 下面是文件里面默认允许的 ip 范围
# IPv4 local connections:
host    all         all         127.0.0.1/32          trust
# IPv6 local connections:
host    all         all         ::1/128               ident

# 为了方便我直接改成了全部都允许，如下所示：
# IPv4 local connections:
host    all         all         all                   trust
# IPv6 local connections:
host    all         all         all                   ident
```

然后另一个文件这么改：

```sh
# 旧版本的 conf 文件在 /var/lib/pgsql/data/ 下
$ sudo vi /var/lib/postgres/data/postgresql.conf

# 下面是文件里面默认监听的 ip
listen_addresses = 'localhost'

# 为了方便同样我也把它改成了监听所有
listen_addresses = '*'
```

然后重启数据库服务，即可远程连接上去啦。