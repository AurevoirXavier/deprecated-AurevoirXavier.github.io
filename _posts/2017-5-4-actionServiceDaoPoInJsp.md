---
layout: post
title: "Action, Service, DAO and PO in Jsp"
date:   2017-05-4
excerpt: "Jsp 中的 action，service，dao 和 po"
tags: [java, jsp, program]
comments: true
---

## Action:

**Action** 类是用户请求和业务逻辑之间的桥梁，每个 **Action** 充当客户的一项业务代理。是 **MVC**模式中 **Control** 层。

## Service:

**Service** 层是在 **MVC** 三层模式中新添加一层，能够更加清晰的定义应用程序的边界，需要操作数据的时候，通过 **Service** 层访问 **DAO** 层来实现。**Service** 层做的事情，不仅仅是调用 **DAO** 操作数据，还会包含了一定的业务逻辑。整个程序的设计，也变成了针对服务进行设计。

## DAO：

*Data Access Object* 是一个数据访问接口，数据访问：顾名思义就是与数据库打交道。夹在业务逻辑与数据库资源中间。是 **MVC** 模式中 **Model** 层。

## PO：

*Persistent Object* 即持久对象，它们是由一组属性和属性的 `get()` 和 `set()` 方法组成。可以看成是与数据库中的表相映射的 **Java** 对象。