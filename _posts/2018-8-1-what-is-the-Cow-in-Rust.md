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

今天在写一个 parser 的时候，第一个目标就是可以读写 xml 。那么上 [crates.io](https://crates.io) 搜索了一波现成的轮子，发现比较受好评的有 [xml-rs](https://crates.io/crates/xml-rs) 和 [quick-xml](https://crates.io/crates/quick-xml) 。前者功能更强大，后者则注重高性能。我选择了后者，因其号称高性能就连名字里也有个 quick，我想这一定很 quick。



关于其 **reader** 的特性介绍有这么一句：is almost zero-copy (use of `Cow` whenever possible)，意思大概就是几乎做到零拷贝，而这零拷贝同时也是其高性能原因之一背后的秘密看来就是这个 `Cow` 了。



接着我们翻一下源码，发现它是一个枚举类型，定义如下：

```rust
pub enum Cow<'a, B: ?Sized + 'a> 
	where B: ToOwned 
{
    Borrowed(&'a B),
    Owned(<B as ToOwned>::Owned),
}
```

*读的懂的可以跳过下面的三个排疑*

1. `where` 是什么？其实它等价于：

   - ```rust
     pub enum Cow<'a, B: ?Sized + 'a + ToOwned> {
         Borrowed(&'a B),
         Owned(<B as ToOwned>::Owned),
     }
     ```

2. `?Sized` 是什么？

   - 事实上，所有形参都隐式地添加了一个约束 `Sized` 以此标记这个形参在编译时大小是可知的，而 `?Sized` 等于取消了这个约束 

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

`Cow<B>` 能直接调用 `B` 的不可变方法，因为它实现了 `Deref` 是一个智能指针。`Borrowed` 只拥有一个不可变的引用，如果你想要可变的话，你必须先克隆然后转换为 `Owned`。然而当你翻阅 `to_mut()` 源码后，发现这正是它所做的事情：

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

如果 `Cow` 已经是 `Owned` 那么它直接返回一个可变 **引用**，并且多次调用只发生一次克隆。`B` 必须以某种方式实现 `ToOwned`。对于那些实现了 `Clone` 的类型，会有一个默认的 `ToOwned` 实现。此外，有一个专门实现的例子，通过复制将 `&str` 转变为 `String`。



使用 `into_owned()` 同样可以得到可变的对象，但是稍有不同，我们再翻翻源码：

```rust
pub fn into_owned(self) -> <B as ToOwned>::Owned {
    match self {
        Borrowed(borrowed) => borrowed.to_owned(),
        Owned(owned) => owned,
    }
}
```

先看对于 `Owned` 的匹配，和前一个方法几乎一样，如果 `Cow` 已经是 `Owned` 那么它直接返回一个 **对象**（是否可变由你掌控）。但如果是 `Borrowed` 的话，源码中可以看到调用了 `to_owned()` 做了一次克隆并返回这个克隆对象。另外还有一点要注意，`into_owned()` 的参数是 `self` 而不是 `&self`，这说明会消耗掉调用它的 `Cow`，所以就不能像 `to_mut()` 一样多次调用了，后面也不能再使用该对象。

## 应用场景

它的全称是 Clone on write（写时克隆）的缩写，所以对于读多写少的场景非常合适。假如你刚爬了一堆代理 ip，有些开头带 http/https 而有些则是纯 ip，你想把全部都改成纯数字。这有什么难的：

```rust
let address_1: String = String::from("http://127.0.0.1");
let address_2: &str = "http://127.0.0.1";

fn pure_ip_1(address: String) -> String {
    if address.contains('s') { return address[8..].to_string(); }
    
    match address.chars().next() {
        Some('h') =>  address[7..].to_string(),
        _ => address,
    }
}

fn pure_ip_2(address: String) -> String {
    if address.contains('s') { return address[8..].to_string(); }

    match address.chars().next() {
        Some('h') =>  address[7..].to_string(),
        _ => address.to_string(),
    }
}
```

那么问题来了：

1. 传 `address_1` 给 `pure_ip_1` 会被直接消耗掉
2. 传 `address_2.to_string()` 给 `pure_ip_1` 做了一次克隆
3. 传 `&address_1` 给 `pure_ip_2` 如果已经是纯 ip，即使不做修改也要克隆再返回
4. 传 `address_2` 给 `pure_ip_2` 如果已经是纯 ip，即使不做修改也要克隆再返回

此时 `Cow` 便是万全之策，为了避免问题 1 2 传入 `&str`，为了避免问题 3 4 我们返回 `Cow<str>`：

```rust
use std::borrow::Cow;

fn pure_ip_3<'a>(address: &'a str) -> Cow<'a, str> {
    if address.contains('s') { return Cow::Owned(address[8..].to_owned()); }

    match address.chars().next() {
        Some('h') => Cow::Owned(address[7..].to_owned()),
        _ => Cow::Borrowed(address),
    }
}

fn pure_ip_4(address: &str) -> Cow<str> {
    if address.contains('s') { return Cow::Owned(address[8..].to_string()); }

    match address.chars().next() {
        Some('h') => Cow::Owned(address[7..].to_string()),
        _ => Cow::Borrowed(address),
    }
}
```

`pure_ip_3` 是最初版本，与 `pure_ip_4` 有两处不同：

1. 由于现在编译器能推断这种简单的生命周期，所以可以省略生命周期参数 `‘a`
2. 详见 [to_owned() 与 to_string()](https://uvwvu.xyz/Rust/to_owned-and-to_string.rs)

