---
layout: post
title: "Unable to start PostgreSQL"
date:   2018-03-16
excerpt: "无法启动 PostgreSQL 数据库"
tags: [PostgreSQL]
comments: true
---

```sh
 $ sudo systemctl start postgresql
    Job for postgresql.service failed because the control process exited with error code.
    See "systemctl status postgresql.service" and "journalctl -xe" for details.
```

一般这个问题是出现在第一次安装完成后，原因是没有初始化。

所以我们需要以下几个步骤来初始化以下数据库：

```sh
# 创建数据存放的文件夹
$ sudo mkdir /var/lib/postgres/data

# 将刚创建的文件夹所有权交给 postgres 用户
$ sudo chown postgres /var/lib/postgres/data

# 用 postgres 用户启动数据库初始化
$ sudo -i -u postgres
$ initdb -D '/var/lib/postgres/data'

# 启动数据库服务
$ sudo systemctl start postgresql
```

至此，数据库就可以成功启动了。

特别提醒一下有些旧版本需要把上面步骤中的路径改为 `/var/lib/pgsql/data`。如果你使用的是最新版，那么照我的来就可以了。