---
layout: post
title: "difference between Clone and Copy"
date:   2018-10-7
excerpt: "Clone 与 Copy 的区别"
tags: [Rust]
comments: true
---

<center><h2>Clone 与 Copy 的区别</h2></center>

<!--more-->

`Clone` 主要是用来应付各种复制的，与 `Copy` 最大的区别在于使用时候是显式的而非隐式的，比如说：

```rust
[test]
fn clone_copy() {
    {
        let a: usize = 0;
        let b = a;

        println!("a: {}, b: {}", a, b);
    }

    {
        let a: Vec<usize> = vec![];
        let b = a;
        // let b = a.clone();

        println!("a: {:?}, b: {:?}", a, b); // error: value moved
    }
}
```

为什么第一个例子不会出现 *value moved*，就是因为其实现了 `Copy`，`b` 是与 `a` 复制出来的对象绑定。而第二个例子中，`b` 与 `a` 指向的 `Vec` 绑定了，因此 `a` 的使命就结束了，后面无法再对 `a` 进行任何操作，所以如果想要复制的话就需要显式的手动调用 `clone()` 了。

也许你会想，为什么不全部做成 `Copy` 的？但是那样一来，所有都是自动复制的对于内存开销就非常大了，有时候你并不需要复制，而对于一些简单类型实现并不会带来多少性能上的负担同时带来许多方便。

顺便我们翻一下 `Clone` 的部分源码：

```rust
#[stable(feature = "rust1", since = "1.0.0")]
#[lang = "clone"]
pub trait Clone : Sized {
    /// Returns a copy of the value.
    ///
    /// # Examples
    ///
    /// ```
    /// let hello = "Hello"; // &str implements Clone
    ///
    /// assert_eq!("Hello", hello.clone());
    /// ```
    #[stable(feature = "rust1", since = "1.0.0")]
    #[must_use = "cloning is often expensive and is not expected to have side effects"]
    fn clone(&self) -> Self;

    /// Performs copy-assignment from `source`.
    ///
    /// `a.clone_from(&b)` is equivalent to `a = b.clone()` in functionality,
    /// but can be overridden to reuse the resources of `a` to avoid unnecessary
    /// allocations.
    #[inline]
    #[stable(feature = "rust1", since = "1.0.0")]
    fn clone_from(&mut self, source: &Self) {
        *self = source.clone()
    }
}
```

其中也指出了 **克隆非常昂贵，但是它应该不会有副作用（cloning is often expensive and is not expected to have side effects）**。然后我们再看一眼 `Copy` 的部分源码：

```rust
#[stable(feature = "rust1", since = "1.0.0")]
#[lang = "copy"]
pub trait Copy : Clone {
    // Empty.
}
```

发现了什么？`Copy` 继承于 `Clone`！是不是发现上面所说的更好理解了？