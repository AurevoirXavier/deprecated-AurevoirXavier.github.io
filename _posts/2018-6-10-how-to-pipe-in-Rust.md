---
layout: post
title: "How to pipe in Rust"
date:   2018-06-10
excerpt: "如何在 Rust 中实现管道符号"
tags: [Rust]
comments: true
---

<center><h2>如何在 Rust 中实现管道符号</h2></center>

<!--more-->

某些时候我们需要使用一些系统命令，于是有了 `std::process::Command`，它类似于 **Python** 的 `os.system()`。但有些时候我们需要管道符号的功能，比如 `mail` 命令的 `echo` 用法。这里用 `ls -la  | rg rs`（`rg` 是一个用 **Rust** 实现的 `grep` 并且更加好用，你可以使用 `cargo install ripgrep` 安装它）做一个例子：

```rust
fn main() {
    use std::io::Write;
    use std::process::{Command, Stdio};

    let output = Command::new("ls")
        .arg("-l")
        .arg("-a")
        .output()
        .unwrap();
    
    let mut child = Command::new("rg")
        .stdin(Stdio::piped())
        .spawn()
        .unwrap();

    {
        let stdin = child.stdin.as_mut().unwrap();
        
        stdin.write_all(&output.stdout).unwrap();
    }

    let output = child.wait_with_output().unwrap();
    
    println!("{}", String::from_utf8_lossy(&output.stdout));
}
```

1. 使用 `Command::new("ls")` 产生一个命令
2. 使用 `arg()` 传入参数，也可以使用 `args(&["-l", "-a"])` 一次传入多个参数
3. 使用 `output()` 执行命令并获取其输出
4. 新建一个命令 `Command::new("rg")`，这里需要绑定为可变 `mut`
5. 使用 `stdin()` 获取一个标准输入的句柄
6. 传入 `Stdio::piped()` 连接父进程和子进程
7. 使用 `spawn()` 执行，与 `output()` 最大的不同就是以子进程形式来执行
8. 传入输入，特别注意 `as_mut()`，如果不使用的话会获取 `child` 变量的所有权，后面无法再使用，不过本例中无关痛痒
9. 使用 `wait_with_output()`，不然会让子进程一直处于读取状态导致程序假死

如果再深入一点的话，你完全可以用这些知识来构建一个可交互的终端，可以参考这里 [stackoverflow](https://stackoverflow.com/questions/31576555/unable-to-pipe-to-or-from-spawned-child-process-more-than-once)。