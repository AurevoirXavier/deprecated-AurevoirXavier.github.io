---
layout: post
title: "to_owned() and to_string()"
date:   2018-06-07
excerpt: "to_owned() 与 to_string()"
tags: [Rust]
comments: true
---

<center><h2>to_owned() 与 to_string()</h2></center>

<!--more-->

可能经常会见到用 `to_owned()` 或者 `to_string()` 去转换一个字符串常量（`&str`）为 `String`，为什么会用两种不同的方法？我们需要将其分为三个问题来一步步讨论。

**应该使用哪种？**

旧版本中应该使用 `to_owned()`，新版本中应使用 `to_string()` 。原因见第三问。
·
---

**它们转换过程中分别发生了什么？**

1. `to_string()` 
   - 对于所有实现了 `ToString trait` 的类型进行了一个转换。它使用格式化函数，因此可能最终进行多次分配并运行更多的代码。
2. `to_owned()`
   - 只分配一个缓冲区并将常量复制到缓冲区中。

显然，`String` 和 `＆str` 都是字符串，但其中的区别在于你是否拥有它：

```rust
fn need_string(s: String) {}

let s = "I'm a &str";

// 现在我手头上有一个借用的字符串，因此我需要一个字符串，但是...为什么
need_string(s.to_string());

// 现在我手头上有一个借用的字符串，因此我需要拥有它
need_string(s.to_owned());

```

---

**为什么都有人采用？**

时至今日，对于 [`str::to_string()` 的特化 405](https://github.com/rust-lang/rust/pull/32586) 已经完成。可以确保 `to_owned()` 与 `to_string()` 的性能完全相同。因此我们现在应该使用 `to_string()`，因为它有更好的可读性，一看就知道这是一个转换为 `String` 的操作。