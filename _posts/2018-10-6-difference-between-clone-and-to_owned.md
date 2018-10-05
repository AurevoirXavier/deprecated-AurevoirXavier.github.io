---
layout: post
title: "difference between clone() and to_owned()"
date:   2018-06-13
excerpt: "clone() 与 to_owned() 的区别"
tags: [Rust]
comments: true
---

<center><h2>clone() 与 to_owned() 的区别</h2></center>

<!--more-->

简单来说 `clone()` 返回他的调用者，比如你对 `&str` 做克隆，返回的就是 `&str`。

在绝大多数情况下 `clone()` 都能够满足你的需求，不过遇到像上面的情况就需要请 `to_owned()` 出马了。

造成这种现象根本原因是 `clone()` 对于 `str` 是实现在其引用类型上的，不信你可以对 `&str` 解引然后让其调用 `clone()`，此时编译器会提示没有 `clone()` 方法。

上述所有情况都包含在下面的例子中了：

```rust
#[test]
fn clone_and_to_owned() {
    use std::mem;
    
    let s1: &'static str = "s1";
    let s2 = "s2".to_string();
    
    {
        let c1 = s1.clone(); 
        let c2 = s2.clone();
        
        println!("{}", c1 == s1);
        println!("{}", c2 == s2);
        println!("{}", mem::size_of_val(c1));
        println!("{}", mem::size_of_val(c2)); // error: expected reference, found struct`std::string::String`
    }
    
    {
        let o1 = s1.to_owned();
        let o2 = s2.to_owned();
        
        println!("{}", o1 == s1);
        println!("{}", o2 == s2);
        println!("{}", mem::size_of_val(o1)); // error: expected reference, found struct`std::string::String`
        println!("{}", mem::size_of_val(o2)); // error: expected reference, found struct`std::string::String`
    }

    {
        println!("{}", mem::size_of_val((*s1).clone())); // error: no method named `clone` found for type `str` in the current scope
    }
}
```