---
layout: post
title: "How to match a String in Rust"
date:   2018-06-01
excerpt: "Rust 中如何对 String 进行模式匹配"
tags: [Rust]
comments: true
---

<center><h2>Rust 中如何对 String 进行模式匹配</h2></center>

<!--more-->

首先最直接的想法是这样：

```rust
fn main() {
    let str = String::from("foo");
    
    match str {
        "foo" => println!("matched"),
        _ => unreachable!()
    }
}

// 编译会得到一个类型不匹配的错误，显而易见上面的代码尝试使用 &str 来匹配 String
// error[E0308]: mismatched types
// note: expected type `std::string::String`
//          found type `&'static str`
```

*这里给出 [E0308](https://doc.rust-lang.org/error-index.html#E0308) 的详细解释*

不过对于 **Rust** 有一定基础的人会先这么想到：

```rust
fn main() {
    let str = String::from("foo");
    
    match str {
        "foo".to_string() => println!("matched"),
        _ => unreachable!()
    }
}

// 这个错误不用编译 ide 都能检测到
// 原因是有一个句点，这个语法在此处是没有意义的，常见的有 `=>` `@` `|` 这些
```

既然不能通过 `.` 来调用方法，可能又会想到这么一招奇技淫巧：

```rust
fn main() {
    let str = String::from("foo");
    
    match str {
        String::from("foo") => println!("matched"),
        _ => unreachable!()
    }
}

// 很遗憾，这也是不行的，编译会得到
// error[E0164]: expected tuple struct/variant, found method `<String>::from`
// 意思就是你尝试以结构体或者枚举去匹配一个并非前面所述两者其中之一的情况
```

*这里给出 [E0164](https://doc.rust-lang.org/error-index.html#E0164) 的详细解释*

---

接下来会提供 **4** 种解决方法：

**1.**

```rust
fn main() {
    let str = String::from("foo");
    
    match str.as_ref() {
        "foo" => println!("matched"),
        _ => unreachable!()
    }
}
```

**2.**

```rust
fn main() {
    let str = String::from("foo");
    
    match str.as_str() {
        "foo" => println!("matched"),
        _ => unreachable!()
    }
}
```

**3.**

```rust
fn main() {
    let str = String::from("foo");
    
    match &str[..] {
        "foo" => println!("matched"),
        _ => unreachable!()
    }
}
```

**4.**

```rust
fn main() {
    let str = String::from("foo");
    
    match &str as &str {
        "foo" => println!("matched"),
        _ => unreachable!()
    }
    
    // 如果两个 &str 把你搞头晕了可以这么写
    let s = String::from("foo");
    
    match &s as &str {
        "foo" => println!("matched"),
        _ => unreachable!()
    }
}
```

四个方法大同小异，都是在匹配之前进行一个转换。特别说一下，第三个是转为 `slice（切片）`来操作。也许对前两个转换方法的本身有疑问？可以看 [Borrow and AsRef](https://uvwvu.xyz/Rust/Borrow-and-AsRef.rust)。