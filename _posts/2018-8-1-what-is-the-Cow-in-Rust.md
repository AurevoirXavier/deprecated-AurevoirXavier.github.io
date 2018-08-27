---
layout: post
title: "What's the Cow in Rust"
date:   2018-8-1
excerpt: "Rust 中的 Cow 是什么"
tags: [Rust]
comments: true
---

<center><h2>Rust 中的 Cow 是什么</h2></center>

<!--more-->



## 什么是 Cow

今天在写一个 parser 的时候，第一个目标就是可以读写 xml 。那么上 [crates.io](https://crates.io) 搜索了一波现成的轮子，发现比较受好评的有 [xml-rs](https://crates.io/crates/xml-rs) 和 [quick-xml](https://crates.io/crates/quick-xml) 。前者功能更强大，后者则注重高性能。我选择了，因其号称高性能就连名字里也有个 quick，我想这一定很 quick。



关于其 **reader** 的特性介绍有这么一句：is almost zero-copy (use of `Cow` whenever possible)，意思大概就是几乎做到零拷贝，而这零拷贝同时也是其高性能原因之一背后的秘密看来就是这个 `Cow` 了。



接着就翻一下源码，发现它是一个枚举类型，定义如下：

```rust
pub enum Cow<'a, B: ?Sized + 'a> 
	where B: ToOwned 
{
    Borrowed(&'a B),
    Owned(<B as ToOwned>::Owned),
}
```

*读的懂的可以跳过下面的简单说明*

1. `where` 是什么？其实它等价于：

   - ```rust
     pub enum Cow<'a, B: ?Sized + 'a + ToOwned> {
         Borrowed(&'a B),
         Owned(<B as ToOwned>::Owned),
     }
     ```

2. `?Sized` 是什么？

   - 事实上，所有形参都隐式地添加了一个约束 `Sized` 以此标记这个形参在编译时大小是可知的，而 `?Sized` 等于取消了这个约束。 

3. `<B as ToOwned>::Owned` 是什么？其实它等价于：

   - ```rust
     pub enum Cow<'a, B>
     where
         B: 'a + ToOwned + ?Sized,
     {
         Borrowed(&'a B),
         Owned(B::Owned),
     }
     ```

   1. `as` 在此处的用法官方称之为[完全限定语法](https://doc.rust-lang.org/book/second-edition/ch19-03-advanced-traits.html#fully-qualified-syntax-for-disambiguation-calling-methods-with-the-same-name)，用于处理重名问题
   2. 这一整句就是你如何访问 `B` 关于 `ToOwned` 的实现的语法

`Borrowed` 只拥有一个不可变的引用，如果你想要可变引用的话，你必须先克隆然后转换为 `Cow` 为 `Owned`。然而当你翻阅 `to_mut()` 源码后，这正是它所做的事情：

```rust
pub fn to_mut(&mut self) -> &mut <B as ToOwned>::Owned {
        match *self {
            Borrowed(borrowed) => {
                *self = Owned(borrowed.to_owned());
                match *self {
                    Borrowed(..) => unreachable!(),
                    Owned(ref mut owned) => owned,
                }
            }
            Owned(ref mut owned) => owned,
        }
    }
```

如果 `Cow` 已经是 `Owned` 那么返回一个可变引用。

## 应用场景