---
layout: post
title: "current transaction is aborted in PostgreSQL"
date:   2018-03-17
excerpt: "ERROR: current transaction is aborted"
tags: [PostgreSQL, Python]
comments: true
---

<center><h2>ERROR: current transaction is aborted</h2></center>

<!--more-->

这个错误是在事务中某个 sql 语句执行错误后没有 `rollback` 或者 `commit`，然后继续执行其他 sql 导致的。而且这个问题大多数出在与程序的交互中，因为当你直接操作数据库的时候它是默认开启了 `AUTOCOMMIT`（自动提交），当你直接操作数据库时输错了什么后结果都会直接出现在终端里面。不过如果你想关掉这个功能可以：`\set AUTOCOMMIT off`。

稍微举个例子（这里我用 `python` 因为写起来比较方便）：

```python
# 导入与 PostgreSQL 交互的模块
import psycopg2

# 连接数据库，密码当然不给你看啦
connect = psycopg2.connect(database="test", user="aurevoirxavier", password="■", host="arch-linux", port="5432")

# 创建一个 cursor
cursor = connect.cursor()

# 删掉 test 数据库中的 users 表（不过我没有这个表）
cursor.execute('drop table users')

# 提示我出错了，没有这个表
---------------------------------------------------------------------------
ProgrammingError Traceback (most recent call last)
<ipython-input-4-e372e4762490> in <module>()
----> 1 cursor.execute('drop table users')

ProgrammingError: table "users" does not exist
---------------------------------------------------------------------------

# 没有的话那就创建一个
cursor.execute('CREATE TABLE user_table(id integer, name VARCHAR(20));')

# 出现了本文的核心问题了
---------------------------------------------------------------------------
InternalError Traceback (most recent call last)
<ipython-input-5-f3bd13458c1f> in <module>()
----> 1 cursor.execute('CREATE TABLE user_table(id integer, name VARCHAR(20));')

InternalError: current transaction is aborted, commands ignored until end of transaction block
---------------------------------------------------------------------------

# 你再执行更多的 sql 语句都是这个结果因为前一条出错了，不能放着不管
# 这时候你有两个选择 commit 或者 rollback
# commit 的话数据库那边会出一个错误信息告诉你 users 不存在
# rollback 的话就恢复到你这次未提交输入的所有命令之前
# 顺便说一下，就算是 commit 的话，你前面所有正确 sql 语句也都作废
# 那么我们选择 rollback 吧，不让数据库出错误日志
connect.rollback()

# 这时候再执行创建条命令，发现可以执行了
cursor.execute('CREATE TABLE user_table(id integer, name VARCHAR(20));')

# 但这时候数据库里面并没有出现新的表，所以你需要 commit
connect.commit()
```

`commit` 和 `rollback` 都可以解决问题，但既然出错了我们就尽量 `rollback`。