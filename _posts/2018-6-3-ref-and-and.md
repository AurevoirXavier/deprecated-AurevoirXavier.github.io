---
layout: post
title: "ref and &"
date:   2018-06-03
excerpt: "ref 与 &"
tags: [Rust]
comments: true
---

<center><h2>ref 与 &amp;</h2></center>

<!--more-->

`ref` 一般用于模式匹配当中，但我们先举几个简单但不常用的例子：

```rust
// 首先，下面这两句话的意义是完全相同的
let x = &y;
let ref x = y;

// 不过，下面这两句话稍有变化
let mut x = &y;         // 创建一个指针，指针自身是可以变的，可以指向其他地方
let ref mut x = &y;     // 这个用法非常少见，创建了一个指向可变的 y 的指针，你可以通过它改变 y，但是不能使它指向其他地方
let x = &mut y;         // 完全等价于上一行

// 这时候，有人会想要一个指向可变内容的可变指针
let mut ref mut x = &y; // 很遗憾，这行不通，语法解析将会卡在 mut 后面紧跟一个 ref 上
let mut x = &mut y;     // 但是这样就可以得到一个指向可变内容的可变指针了
```

通过上面大致了解了两者的功能，下面来说一下 `ref` 最常被用到的地方：

```rust
let foo = 1u32;
let bar = Some(&foo);

match bar {
    Some(&v) => {} // 这里发生了解构，v = foo
}

let bar = Some(foo);

match bar {
    Some(ref r) => {} // 这里是 r = &foo
}
```

仔细思考 `bar` 这个变量，会对理解有所帮助。

---

**自己动手试试：**

下面这个程序会打印出 `val` 的内存占用大小。如果打印出的结果是 **8** 说明 `val` 此时指向一个**指针**，如果打印结果是 **24** 说明此时指向一个 `Vector`。

顺便一提，你可以同时打印 `v` 的占用大小帮助理解。

再顺便一提 `size_of_val()` 函数需要的是一个引用做参数，但返回的不是那个引用自身的内存占用大小，不要搞混了。举个比较随便的例子，通过身份证号得到的出生年月是属于一个人的，并不是身份证的。

在我留下下划线的地方尝试修改为 `ref` 或者 `&` 甚至 `*`，这里有多种组合，耐心尝试，然后你会有所收获。

```rust
fn main() {
    let __ v = __ vec![1, 2, 3];
    
    match __ v {
        __ val => println!("{}", std::mem::size_of_val( __ val))
    }
}
```

先稍微抛砖引玉一下：

```rust
fn main() {
    let v = &vec![1, 2, 3];
    
    // v 指向 Vector，val = v，得到 Vector 的大小
    match v {
        val => println!("{}", std::mem::size_of_val(val))
    }
    
    // v 指向 Vector，val = &v，得到指向 Vector 的指针的大小
    match v {
        ref val => println!("{}", std::mem::size_of_val(val))
    }
    
    // v 指向 Vector，val = &v，解引 val，得到 Vector 的大小
    match v {
        ref val => println!("{}", std::mem::size_of_val(*val))
    }
    
    // 解引 v，v = vec![1, 2, 3]，val = &v，得到 Vector 的大小
    match *v {
        ref val => println!("{}", std::mem::size_of_val(val))
    }
    
    // 解引 v，v = vec![1, 2, 3]，val = &v，传入 &val，得到指向 Vector 的指针的大小
    match *v {
        ref val => println!("{}", std::mem::size_of_val(&val))
    }
}
```

不过仍有很多情况没有列举出，有待各位尝试。