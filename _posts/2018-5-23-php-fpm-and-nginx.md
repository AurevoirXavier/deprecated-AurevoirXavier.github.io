---
layout: post
title: "Get start with postgresql"
date:   2018-05-23
excerpt: "postgresql 基本指令"
tags: [postgresql]
comments: true
---

前面讲了安装后的启动和如何远程连接，这次讲几个基本命令。

```sh
# 以 postgres 用户的身份连接数据库，由于没有写数据库名字，默认连接至同名数据库 postgres
sudo -u postgres psql

# 新建 ax 用户，密码为 password
CREATE USER ax WITH PASSWORD 'password';

# 新建数据库 ax，所有者为 ax
CREATE DATABASE ax OWNER ax;

# 提权，不然 ax 用户啥也干不了
GRANT ALL PRIVILEGES ON DATABASE exampledb to dbuser;

# 下面一些是 postgresql 特有的简洁指令
\h：                查看SQL命令的解释，比如\h select。
\?：                查看psql命令列表。
\l：                列出所有数据库。
\c [database_name]：连接其他数据库。
\d：                列出当前数据库的所有表格。
\d [table_name]：   列出某一张表格的结构。
\du：               列出所有用户。
\e：                打开文本编辑器。
\conninfo：         列出当前数据库和连接的信息。
```

至于增删改查，跟其他数据库差不多，就不列举了。