---
layout: post
title: "Borrow and AsRef"
date:   2018-06-02
excerpt: "Borrow 与 AsRef"
tags: [Rust]
comments: true
---

<center><h2>Borrow 与 AsRef</h2></center>

<!--more-->

### 首先我们来看看 `AsRef` 的定义是啥：

[官方文档](https://doc.rust-lang.org/nightly/std/convert/trait.AsRef.html)中的解释大概可以理解为：

它是一个**廉价（开销非常低）**的 **引用->引用** 的转换。和 `Borrow` 非常相似，但用途稍有不同。

当你打算把一类型的引用转换成另一类型的引用时，你应该使用 `AsRef`。

`Borrow` 则更关注于其引用的概念。当你希望在引用类型（`&T, &mut T`）上进行抽象，或者允许以同样的方式去处理引用和拥有类型（**owned type**）时，你应该使用它。

两者的区别体现在于使用的意图：

选择 `AsRef` 当你想要直接把一些值转换为引用，和当你在写泛型代码的时候。

选择 `Borrow` 当你想要抽象不同类型的借用，或者当你创建一个数据结构它把自我拥有和借用的值看作等同的，例如哈希和比较。

想要了解更多信息可以读一下这本[书](https://doc.rust-lang.org/book/first-edition/borrow-and-asref.html)。

---

### 下面换个通俗点的说法：

对于文件系统路径 - 总是使用 `AsRef <Path>`，因为它可以是 `Path` 类型，常规的 **UTF-8 字符串**类型或**系统特定的字符串**类型。

如果所有权无关紧要，请使用 `AsRef`。带有 `AsRef` 参数的函数将同时采用 `foo(obj)` 和 `foo(＆obj)` 而不冲突。当你使用 **Trait** 时通常也很有用 - 你可以使用引用而不必加上生命周期注释。

缺点是它使类型推断更加模糊，因此有时编译器无法确定是否需要将 `＆Vec` 或 `Vec` 转换为 `＆[]`。但一般来说你的目的总是后者，所以对于 `Vector` 使用 `＆[T]` 而不是 `AsRef`。