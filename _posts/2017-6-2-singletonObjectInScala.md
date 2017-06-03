---
layout: post
title: "Scala's singleton object"
date:   2017-06-02
excerpt: "Scala 之单例对象"
tags: [program, scala]
comments: true
---

**Scala** 比 **Java** 更面向对象的一个方面是 **Scala** 没有静态成员。作为弥补，**Scala** 有单例对象：singleton object。

当单例对象与某个类共享同一个名称时，他被称作是这个类的伴生对象：*companion object*。你必须在同一个源文件里定义类和它的伴生对象。类被称为是这个单例对象的伴生类：*companion class*。类和它的伴生对象可以互相访问其私有成员。

类和单例对象间的一个差别是，单例对象不带参数，而类可以。因为你不能用 `new` 关键字实例化一个单例对象，你没机会传递给它参数。每个单例对象都被作为由一个静态变量指向的虚构类：*synthetic class* 的一个实例来实现，因此它们与 **Java** 静态类有着相同的初始化语法。**Scala** 程序特别要指出的是，单例对象会在第一次被访问的时候初始化。

Example：

```scala
class Demo {
}

class A{
    def apply() = println("class A")
    def test: Unit ={
        println("class A -> apply()")
    }
}

object A{
     def apply() = {
          println("object A")
        new A
     }
}

object Demo {
     def main (args: Array[String]) {
        val a = A()

         a.test
         a()
    }
}
```

