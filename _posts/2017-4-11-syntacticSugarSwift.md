---
layout: post
title: "Syntactic sugar (Swift)"
date:   2017-04-11
excerpt: "Swift 中的一些语法糖"
tags: [program, swift]
comments: true
---

## 什么是 Syntactic sugar ？

语法糖 (Syntactic sugar)，也译为糖衣语法，是由英国计算机科学家彼得·约翰·兰达 (Peter J. Landin) 发明的一个术语，指计算机语言中添加的某种语法，这种语法对语言的功能并没有影响，但是更方便程序员使用。通常来说使用语法糖能够增加程序的可读性，从而减少程序代码出错的机会。语法糖和其他编程思想一样重要，什么 *duck type*，人本接口，最小接口，约定优于配置，广义来讲都是一些思想上的“语法糖“。需要声明的是 “语法糖” 这个词绝非贬义词，它可以给我们带来方便，是一种便捷的写法，编译器会帮我们做转换；而且可以提高开发编码的效率，在性能上也不会带来损失。

## if let

```swift
func printX(str: String?)
{
    let x: String! = str
    
    if x != nil
    {
     	print(x)   // 做些什么，比如输出一下 x
    }
}
```

**Swift** 中有 **optional**，经常需要判断其是否为空。如果不使用 `if let`，`printX()` 写出来是上面那样，使用了 `if let` 后：

```swift
func printX(str: String?)
{
    if let x = str
    {
     	print(x)   // 做些什么，比如输出一下 x
    }
}
```

## guard

当 `if` 中有较长的代码时，通常先将错误情况先返回，这样做可以避免过多的嵌套。比如：

```swift
func printX(str: String?)
{
    let x: String! = str
    
    if x == nil
    {
     	return
    }
    
    print(x)   // 做些什么，比如输出一下 x
}
```

此处 **Swift** 也提供了一个语法糖 `guard`，用 `guard` 可以改写成：

```swift
func printX(str: String?)
{
    guard let x = str else { return }

    print(x)   // 做些什么，比如输出一下 x
}
```

有关 `if let` 和 `guard` 语法中出现的 `where` (本文例子中未出现)，属于一些约束。相当于逻辑运算 && 和 \|\|。不妨把它看作 **Sql** 中的 `where` 吧。

## Optional ?

一个 **Optional** 值是一个具体的值或者是 `nil` 以表示值缺失。在类型后面加一个 `?` 来标记这个变量的值是可选的：

```swift
var demo: String?   //? 是下面这种写法的语法糖
var demo: Optional<String>
```
