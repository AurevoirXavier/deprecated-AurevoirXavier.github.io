---
layout: post
title: "String and &str"
date:   2018-06-04
excerpt: "String 与 &str"
tags: [Rust]
comments: true
---

<center><h2>String 与 &amp;str</h2></center>

<!--more-->

#### 这里我们需要先谈一谈 *Rust* 中的字符类型

相信从别的编程语言来的人基本都很熟悉 `String` 这个类型，但是到了 *Rust* 中它就有了些变化。而且还有一个 `str` 类型来表示字符串，这就让刚接触 *Rust* 的人有些困扰。

首先 `str` 的官方名字叫做字符串字面值，它是被硬编码进程序中的，说到这里你应该清楚，它是不可变的。所以我们需要多一个字符串类型来满足其他需求，比如说灵活修改内容还有获取用户输入（外来输入这意味着一开始并不知道确切的内容是什么），这就有了 `String`。

这时候你可能会说同样任务交给 `String` 都能完成，`str` 有什么理由的存在，这时候就要说一下它们的内存分配方式了：

- 对于 `str`，在编译时就知道其内容所以它直接被硬编码进最终的可执行文件中，所以它使用起来快速且高效。
- 对于 `String`，为了支持一个可变，可增长的文本片段，需要在堆上分配一块在编译时未知大小的内存来存放内容。

```rust
let s1 = String::from("hello");
let s2 = s1;
```

结合上面的代码，我们来看一看 `String` 究竟长什么样。一共三部分组成，如图左侧所示：一个指向存放字符串内容内存的指针，一个长度，和一个容量。这一组数据储存在栈上。右侧则是堆上存放内容的内存部分。

![String in memory](https://uvwvu.xyz/usr/uploads/2018/07/96721258.svg)

长度代表当前 `String` 的内容使用了多少字节的内存。容量是 `String` 从操作系统总共获取了多少字节的内存。长度与容量的区别是很重要的，不过这在目前为止的场景中并不重要，所以可以暂时忽略容量。

当我们把 `s1` 赋值给 `s2`，`String` 的数据被复制了，这意味着我们从栈上拷贝了它的指针、长度和容量。我们并没有复制堆上指针所指向的数据。换句话说，内存中数据是这样的：

![s1 moved to s2][https://uvwvu.xyz/usr/uploads/2018/07/1189791748.svg]

变量离开作用域后 *Rust* 自动调用 `drop` 函数并清理变量的堆内存。不过上图显示了两个数据指针指向了同一位置。这就有了一个问题：当 `s2` 和 `s1` 离开作用域，他们都会尝试释放相同的内存。这是一个叫做 **二次释放**（*double free*）的错误。两次释放（相同）内存会导致内存污染，它可能会导致潜在的安全漏洞。如果你在其他语言中听说过术语 “浅拷贝”（“shallow copy”）和 “深拷贝”（“deep copy”），那么拷贝指针、长度和容量而不拷贝数据可能听起来像浅拷贝。不过 *Rust* 在 `s2` 被创建的同时使 `s1` 无效化了，这个操作被称为 **移动**（*move*），而不是浅拷贝。上面的例子可以解读为 `s1` 被 **移动** 到了 `s2` 中。图中以涂上阴影的方式来表示被无效化。顺便一提如果你想要深拷贝，只需要使用 `clone()`。

```rust
let s1 = String::from("hello");
let s2 = s1.clone();
```

此时，在内存中看起来是这样：

![s1 and s2 to two places](https://uvwvu.xyz/usr/uploads/2018/07/3155458848.svg)

想更多了解 `String`？查看，[额外内容](https://doc.rust-lang.org/book/second-edition/ch04-01-what-is-ownership.html)。

#### 上面讲了这么多，现在来对比一下 `&String` 和 `&str`

大体上，一个 `String` 包装并管理一个动态分配的 `str` 作为后备存储器。由于 `str` 不能调整大小，所以 `String` 将动态地分配和释放内存。因此 `&str` 是直接进入字符串备份存储的引用，而 `&String` 是对**包装对象**的引用。还有一点，`&str` 可用于子字符串，即它们是 `slices（切片）`，而 `&String` 引用的总是整个字符串。

```rust
let a = "hello";
let b = "hello"[0..3];

println!("{}", &a[0..3]);
```

想更多了解 `str`？查看，[额外内容](https://doc.rust-lang.org/book/second-edition/ch19-04-advanced-types.html#dynamically-sized-types--sized)。