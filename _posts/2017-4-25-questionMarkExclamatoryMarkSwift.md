---
layout: post
title: "? and ! in Swift"
date:   2017-04-25
excerpt: "Swift 中的 ? 和 !"
tags: [syntax, program, swift]
comments: true
---

## 简单值

使用 `let` 来声明常量，使用 `var` 来声明变量。一个常量的值，在编译的时候，并不需要有明确的值，但是你只能 为它赋值一次。也就是说你可以用常量来表示这样一个值：你只需要决定一次，但是需要使用很多次。但 Swift 不会自动给变量赋初始值，也就是说变量不会有默认值，所以要求使用变量之前必须要对其初始化。如果在使用变量之前不进行初始化就会报错：

```swift
var testString: String
//note: variable defined here

let hashValue = testString.hashValue
//error: variable 'testString' used before being initialized
```

## Optional 值

**Optional** 其实是个 `enum`，里面有 `None` 和 `Some` 两种类型。其实所谓的 `nil` 就是 `Optional.None`, 非 `nil` 就是 `Optional.Some`, 然后会通过 `Some(T)` 包装 (**wrap**) 原始值，这也是为什么在使用 **Optional** 的时候要拆包 (**unwrap**: 从 `enum` 里取出来原始值) 的原因, 也是 *PlayGround* 会把 **Optional** 值显示为类似 `{Some "hello world"}` 的原因，以下是 **enum Optional** 的定义：

```swift
enum Optional<</span>T> : LogicValue, Reflectable {
    case None
    case Some(T)
    init()
    init(_ some: T)

    /// Allow use in a Boolean context.
    func getLogicValue() -> Bool

    /// Haskell's fmap, which was mis-named
    func map<</span>U>(f: (T) -> U) -> U?
    func getMirror() -> Mirror
}
```

一个 **Optional** 值是一个具体的值或者是 `nil` 以表示值缺失。在类型后面加一个 `?` 来标记这个变量的值是可选的：

```swift
var strValue: String?   //? 相当于下面这种写法的语法糖
var strValue: Optional<String>
```

<center><a href = “syntacticSugarSwift”>更多 Swift 语法糖点击此</a></center>

