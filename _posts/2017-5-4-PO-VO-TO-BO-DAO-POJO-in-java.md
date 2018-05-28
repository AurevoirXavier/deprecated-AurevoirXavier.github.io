---
layout: post
title: "PO，VO，TO，BO，DAO，POJO in Java"
date:   2017-05-04
excerpt: "Java 中的 PO，VO，TO，BO，DAO，POJO"
tags: [Java]
comments: true
---

<center><h2>Java 中的 PO，VO，TO，BO，DAO，POJO</h2></center>

<!--more-->

#### PO (persistant object) 持久对象

出现在 o/r 映射中的概念，如果没有 o/r 映射，这个概念不存在。通常对应于数据模型 (数据库) ，本身部分是业务逻辑处理。可以映射到数据库中的表对象。最简单的 PO 数据库对应于表中的记录，可以使用多个记录 PO 收集。PO不 应该包含数据库的任何操作。

#### VO (value object) Value 对象

通常用于业务层之间的数据传输，PO 只包含数据。但它应该是抽象的业务对象，而表，也不能，这根据业务的需要。我认为用 DTO (数据传输对象，在 Web 中传输) 。

#### TO (transfer object) ，数据传输对象

在应用不同领带 (关系) 之间的物体传播

#### BO (business object) 业务对象

从商业模式的角度来看，在对象领域中看到 UML 元素的域模型。要封装 Java 对象的业务逻辑，通过调用 DAO 方法，结合 PO，VO 进行业务操作。

#### POJO (plain ordinary java object) 没有简单规则的 Java 对象

传统的纯 Java 对象。也就是说在一些对象/关系映射工具中，可以维护数据库记录persisent对象完全符合J ava 规范的 Bean 纯 Java 对象，而不添加其他属性和方法。我的理解是最基本的 Java Bean，只有属性字段和 setter 和 getter 方法！

#### DAO (data access object) 数据访问对象

是一个标准的 J2EE 设计模式，一个太阳，一个 DAO 接口是操作模式，它的负持续层。为业务层提供接口。此对象用于访问数据库。通常与 PO 结合使用，DAO 包含各种数据库操作方法。通过其方法，结合 PO 对数据库的相关操作。在业务逻辑和数据库资源的中间。使用 VO，提供数据库 CRUD 操作。 

#### O/R Mapper 对象/关系映射

在定义所有映射之后，O/R Mapper 可以帮助我们做很多工作。通过映射，O/R Mapper 可以生成所有关于对象的保存，删除，SQL 语句读取，我们不再需要写这么多行的 DAL 代码。

- 实体模型 (solid) 实体
- DAL (data access layer) 数据访问层
- IDAL (interface) 接口
- DALFactory (factory) 工厂
- BLL (business logic layer) 业务逻辑层
- BOF (business Object Framework business object framework) 业务对象框架业务对象框架
- 面向服务的 SOA Service Orient Architecture 的设计
- EMF Eclipse 模型框架 Eclipse 建模框架

---

#### PO：

图像理解的记录是数据库中的 PO。好处可以把一个记录作为一个对象，对其他对象来说便利。

#### BO：

主要作用是将业务逻辑作为对象进行封装。对象可以包括一个或多个其他对象。例如，简历，教育经历，工作经验，社会关系等。我们可以把教育有相应的 PO，体验相应的 PO，对应 PO 的社会关系。BO 对象处理恢复建立相应的简历，每个 BO 包含 PO。这样的处理业务逻辑，我们可以根据 BO 来处理。

#### VO：

- value object
- view object

数据对象对应界面显示。对于 WEB 页面，接口或 SWT，SWING，具有对应于接口值的 VO 对象。

#### DTO：

主要用于长途电话需要大转移对象的地方。例如，我们有一个表有 100 个字段，那么 PO 有 100 个属性。但是我们的界面只要 10 个显示领域，客户端使用 WEB 服务获取数据，没有必要将 PO 对象传递给客户端，那么我们只能使用 DTO 的这 10 个属性将结果传递给客户端，这也不会暴露给客户端服务器结构。后来，如果你使用这个对象对应的界面显示，那么它的身份就是 VO。

#### POJO：

个人感觉 POJO 是最常见最可变的对象，是一个中间对象，对象是我们最经常处理的。POJO 持久性是 PO，它直接用于转移，转移过程是 DTO，直接对应的表示层是 VO。

#### DAO：

最熟悉的，以上 O 最大的区别，基本上没有可能性和必要转变成对方主要用于封装对数据库的访问。它可以把 POJO 持久化 PO，由 PO VO，DTO 组装。