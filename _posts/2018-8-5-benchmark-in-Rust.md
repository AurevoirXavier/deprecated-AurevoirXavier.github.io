---
layout: post
title: "how to benchmark in Rust"
date:   2018-8-5
excerpt: "在 Rust 中计算耗时的两种姿势"
tags: [Rust]
comments: true
---

<center><h2>在 Rust 中计算耗时的两种姿势</h2></center>

<!--more-->



ipython 中有个 `time()` 方法，可以计算执行时间，非常的方便好用。Rust 中没有这种现成的方法，那么在 Rust 中该怎么办？下面给大家介绍两种方法。

#### cargo bench

虽没有 `time()` 不过取而代之是有一条专用的 `cargo bench` 命令。让我们来看看，如何为你的程序写 **bench**：

```rust
#![feature(test)]

extern crate test;

fn new_vec(len: usize) -> Vec<usize> {
    let mut v = vec![];
    for n in (0..len).rev() {
        v.push(n);
    }

    v.sort();

    v
}

#[cfg(test)]
mod tests {
    use super::new_vec;
    use test::Bencher;
    
    #[bench]
    fn bench_new_vec(b: &mut Bencher) {
        b.iter(|| new_vec(1000000));
    }
}

// test tests::bench_new_vec         ... bench:   7,338,001 ns/iter (+/- 596,449)
```

然后直接 `cargo bench` 就能得出结果了。有时候可能会很久，其中有个原因是测试不仅仅只进行一次而是多次，最后取一个平均值。有时候你的测试可能非常简单，像是这样：

```rust
#![feature(test)]

extern crate test;

#[cfg(test)]
mod tests {
    use super::new_vec;
    use test::Bencher;
    
    #[bench]
    fn bench_square_10_times(b: &mut Bencher) {
    	b.iter(|| {
        	(0..10).fold(1, |acc, _| acc^2);
    	});
    }
}

// test tests::bench_square_10_times ... bench:           0 ns/iter (+/- 0)
```

你可能会问为什么结果是 0，原因在于这个计算结果没有什么外部作用所以整个计算直接在编译的时候被优化掉了。但只要用下面这个小技巧便可得到你想要的：

```rust
#![feature(test)]

extern crate test;

#[cfg(test)]
mod tests {
    use super::new_vec;
    use test::{Bencher, black_box};
    
    #[bench]
    fn bench_square_10_times(b: &mut Bencher) {
        b.iter(|| {
            let n = black_box(10);
            (0..n).fold(0, |acc, _| acc ^ 2)
        });
    }
}

// test tests::bench_square_10_times ... bench:           3 ns/iter (+/- 0)
```

不同之处就是使用了一个黑盒子（障眼法），强制让优化器认为它有用使得其不被优化掉。

#### extern crate time

Rust 标准库一直都是非常精简的，所以 `std::time` 里面的都是一些基础的东西，相当不好用。我们需要在 **Cargo.toml** 中添加 **time** 这个 **crate**：

```rust
[package]
name = "benchmark"
version = "0.1.0"
authors = ["Xavier Lau <c.estlavie@icloud.com>"]

[dependencies]
time = "*"
```

接着我们可以这样写，你可能非常熟悉，因为大部分语言都可以这么写：

```rust
extern crate time;

fn new_vec(len: usize) -> Vec<usize> {
    let mut v = vec![];
    for n in (0..len).rev() {
        v.push(n);
    }

    v.sort();

    v
}

#[cfg(test)]
mod tests {
    use super::new_vec;
    use time::PreciseTime;

    #[test]
    fn time_new_vec() {
        let start = PreciseTime::now();
        new_vec(1000000);
        let end = PreciseTime::now();

        println!("{}", start.to(end));
    }
}

// PT0.112012561S
```

很简单，记录一个起点一个终点，计算时间差，得出执行时间。这时候你可能会问，这里怎么变成 **0.11** 秒了，**bench** 下测出的不是 **0.073** 吗？原因在于你没有打开优化开关，这是测试环境下的结果。测试环境编译快方便 debug 但是缺点如你所见。那么我们在 **Cargo.toml** 中打开优化开关：

```rust
[package]
name = "benchmark"
version = "0.1.0"
authors = ["Xavier Lau <c.estlavie@icloud.com>"]

[dependencies]
time = "*"

[profile.bench]
opt-level = 3
debug = false
rpath = false
lto = false
debug-assertions = false
codegen-units = 16
panic = 'unwind'
incremental = false
overflow-checks = false
```

**profile.bench** 是针对 `cargo test --release` 和 `cargo bench` 优化的。这时候你再运行 `cargo test --release`，是不是结果差不多了？