---
layout: post
title: "String, str and slice"
date:   2018-06-04
excerpt: "String 与 &str"
tags: [Rust]
comments: true
---

<center><h2>String，str 与 slice</h2></center>

<!--more-->

#### 这里我们先来谈一谈 *Rust* 中的字符类型

相信从别的编程语言来的人基本都很熟悉 `String` 这个类型，但是到了 *Rust* 中它就有了些变化。而且还有一个 `str` 类型来表示字符串，这就让刚接触 *Rust* 的人有些困扰。

首先 `str` 的官方名字叫做字符串字面值，它是被硬编码进程序中的，说到这里你应该清楚，它是不可变的。所以我们需要多一个字符串类型来满足其他需求，比如说灵活修改内容还有获取用户输入（外来输入意味着一开始并不知道确切的内容是什么），这就有了 `String`。

这时候你可能会说同样任务交给 `String` 都能完成，`str` 有什么理由的存在，这时候就要说一下它们的内存分配方式了：

- 对于 `str`，在编译时就知道其内容而直接被硬编码进最终的可执行文件中，所以它使用起来快速且高效。
- 对于 `String`，为了支持一个可变，可增长的文本片段，需要在堆上分配一块在编译时未知大小的内存来存放内容。

```rust
let s1 = String::from("hello");
let s2 = s1;
```

结合上面的代码，我们来看一看 `String` 究竟长什么样。一共三部分组成，如图左侧所示：一个指向存放字符串内容内存的指针，一个长度和一个容量。这一组数据储存在栈上。右侧则是堆上存放内容的内存部分。

![String in memory](https://uvwvu.xyz/usr/uploads/2018/07/96721258.svg)

长度代表当前 `String` 的内容使用了多少字节的内存。容量是 `String` 从操作系统总共获取了多少字节的内存。长度与容量的区别是很重要的，不过这在目前为止的场景中并不重要，所以可以暂时忽略容量。

当我们把 `s1` 赋值给 `s2`，`String` 的数据被复制了，这意味着我们从栈上拷贝了它的指针、长度和容量。我们并没有复制堆上指针所指向的数据。换句话说，内存中数据是这样的：

![s1 moved to s2](https://uvwvu.xyz/usr/uploads/2018/07/1189791748.svg)

变量离开作用域后 *Rust* 自动调用 `drop` 函数并清理变量的堆内存。不过上图显示了两个数据指针指向了同一位置。这就有了一个问题：当 `s2` 和 `s1` 离开作用域，他们都会尝试释放相同的内存。这是一个叫做 **二次释放**（*double free*）的错误。两次释放（相同）内存会导致内存污染，它可能会导致潜在的安全漏洞。如果你在其他语言中听说过术语 “浅拷贝”（“shallow copy”）和 “深拷贝”（“deep copy”），那么拷贝指针、长度和容量而不拷贝数据可能听起来像浅拷贝。不过 *Rust* 在 `s2` 被创建的同时使 `s1` 无效化了，这个操作被称为 **移动**（*move*），而不是浅拷贝。上面的例子可以解读为 `s1` 被 **移动** 到了 `s2` 中。图中以涂上阴影的方式来表示被无效化。顺便一提如果你想要深拷贝，只需要使用 `clone()`。

```rust
let s1 = String::from("hello");
let s2 = s1.clone();
```

此时，在内存中看起来是这样：

![s1 and s2 to two places](https://uvwvu.xyz/usr/uploads/2018/07/3155458848.svg)

想更多了解 `String` ？查看，[这里](https://doc.rust-lang.org/book/second-edition/ch04-01-what-is-ownership.html)还有[这里](https://doc.rust-lang.org/book/second-edition/ch08-02-strings.html)。

---

#### 单独说一下 **slice**

**slice** 是一个没有所有权的数据类型，允许你引用集合中一段连续的元素序列，而不用引用整个集合。

下面会涉及 *Rust* 的 `..` **range** 语法。这类似于获取整个 `String` 的引用不过带有额外的 `[starting_index..ending_index]`部分。不同于整个 `String` 的引用，这是一个包含 `String` 内部的一个位置和所需元素数量的引用。`start..end` 语法代表一个以 `start` 开头并一直持续到但不包含 `end` 的 **range**，但是可以也不写 `start` 会取默认值 **0**，`end` 会取最大长度。

使用一个由中括号中的 `[starting_index..ending_index]` 指定的 **range** 创建一个 **slice**，其中 `starting_index` 是包含在 **slice** 的第一个位置，`ending_index` 则是 **slice** 最后一个位置的后一个值。在其内部，**slice** 的数据结构储存了开始位置和 **slice** 的长度，长度对应 `ending_index` 减去 `starting_index` 的值：

```rust
let foo = &"hello"[..]; // foo: &str

// 下面着两种都是无法通过编译的，因为 foo 编译时大小未知，如果想要通过编译，把它们变成引用就可以了
// let foo = "hello"[0..3];            
// let foo = String::from("hello")[0..3];   

let bar: &[i32; 3] = &[1, 2, 3];
let v = vec![1, 2, 3];  // bar: Vec<i32>
let baz = &bar[..];     // baz: &[i32; 3]

// 以上除了 v 之外，都可以称之为 slice。如你所见，slice 不光适用于字符串
```

我们再来从内存层面来看一下 **slice**：

```rust
let s = String::from("hello world");

let hello = &s[0..5];
let world = &s[6..11];
```

![world containing a pointer to the 6th byte of String s and a length 5](https://uvwvu.xyz/usr/uploads/2018/07/581699634.svg)

对于 `let world = &s[6..11];` 的情况，`world` 是一个包含指向 `s` 第 6 个字节的指针和长度值 5 的 **slice**。

想了解更多 **slice** ？查看，[额外内容](https://doc.rust-lang.org/book/second-edition/ch04-03-slices.html)。

---

#### 通过上面的了解，现在来对比一下 `&String`，`&str` 以及 **slice**

大体上，一个 `String` 包装并管理一个动态分配的 `str` 作为后备存储器。由于 `str` 不能调整大小，所以 `String` 将动态地分配和释放内存。因此 `&str` 是直接进入字符串备份存储的引用，而 `&String` 是对 **包装对象** 的引用。还有一点，`&str` 可用于子字符串，即它可以是 `slice（切片）`，而 `&String` 引用的总是整个字符串。

如果是来自 *C* 的程序员可以试着这样理解：

```c
struct str {
   char text[];      // 大小未知
}

struct &str {
   size_t length; 
   const char *text; // 没有所有权
};

struct String {
   size_t length; 
   size_t free_capacity; 
   char *text;       // 动态内存分配发生
}
```

想更多了解 `str` ？查看，[额外内容](https://doc.rust-lang.org/book/second-edition/ch19-04-advanced-types.html#dynamically-sized-types--sized)。

---

#### 最后总结一下

首先，`[T]` 不是 `Vec`，而是 `[T]`。`vec![1, 2, 3]` 的类型为 `Vec`。不能有类型为 `[T]` 的值。它总是间接出现在我们视野中的。注意此处不要和 `[T; size]` 搞混。

退一步来看。

*Rust* 希望能够有效地获取并传递数组的切片。传递 `(&T, usize)` 是一个不错的主意：一个指向第一个元素的指针，以及元素的数量。可以从 **任何** 连续存储中创建其中一个，无论来自何处。例如，`&[T]` 是一个来自其他其他存储的借用切片。这就引出一个问题：如果 `&SOMTHING` 是指向 `SOMETHING` 的指针，那么 `[T]` 本身意味着什么？虽然我们可以简单的理解它为不可变的数组。

`[T]`：一些连续存储的 n 个 `T` 的类型。没有说明它们存储在哪里，谁拥有它们，如何管理它们，等等，只是某个数字存在于某个地方。我们需要 `[T]`，因为可以通过构建它来创建其他更有用的类型，这些类型对于如何存储这些 `T` 是有意义的。

`&[T]` 说它们是被别人借来并拥有的（可能是静态数据段中的字面值）; `Box<[T]>` 说，你拥有它们，并且拥有对它们的独占访问权; `Rc<[T]>` 说所有权是共享的; `[T; 5]` 恰好是拥有的 5 个 `T` 的集合。

这里不得不提一下 `Vec` 存在的原因：建立数组元素的元素是一个很常见的事情。它基本上可以看作 `Box<[T]>`，但是它保留了一些额外的空间，以使它更高效。你可以对它进行切片以获取 `&[T]`，因为你可以对所有连续存储的东西进行切片以获取 `&[T]`。

`String` 和 `str` 本质上是完全相同的，除了必须是 **有效的 UTF-8** 之外。所以 `[T]`/`str` 是基本的构建块。`Vec` 和 `String` 都是建立在它们之上的东西，因为 `[T]` 和 `str` 本身不会做很多事情。

最后最后再总结一下上面的话：

表面上我们看到的:

- `&str` 是 `String` 的切片

本质上:

- `str` 和 `[T]` 是语言本身的组成部分
- `Vec<T>` 和 `String` 是任何人都可以自行定义的两个类型:
  - `Vec<T>` 是大小可变且由堆分配的 `[T]`
  - `String` 是大小可变且由堆分配的 `str`