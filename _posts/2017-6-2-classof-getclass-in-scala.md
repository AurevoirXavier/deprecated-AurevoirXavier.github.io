---
layout: post
title: "classOf and getClass in Scala"
date:   2017-06-02
excerpt: "Scala 中的 classOf 与 getClass"
tags: [Scala]
comments: true
---

<center><h2>Scala 中的 classOf 与 getClass</h2></center>

<!--more-->

```scala
scala> class  A
scala> val a = new A

scala> a.getClass
res2: Class[_ <: A] = class A

scala> classOf[A]
res3: Class[A] = class A
```

`getClass` 方法得到的是 `Class[A]` 的某个**子类**，而 `classOf[A]` 得到是正确的 `Class[A]`。

但是去比较的话，这两个类型是 `equals` 为 `true`：

```scala
scala> a.getClass  == classOf[A]
res13: Boolean = true
```

原因就是：**Java** 里的 `Class<T>` 是不支持协变的，所以无法把一个 `Class[_ < : A]` 赋值给一个 `Class<A>`：

```scala
scala> val c:Class[A] = a.getClass
<console>:9: error: type mismatch;
```