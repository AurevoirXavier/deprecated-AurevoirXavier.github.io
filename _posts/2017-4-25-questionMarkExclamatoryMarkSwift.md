---
layout: post
title: "? and ! in Swift"
date:   2017-04-25
excerpt: "Swift 中的 ? 和 !"
tags: [syntax, program, swift]
comments: true
---

# 简单值

使用 `let` 来声明常量，使用 `var` 来声明变量。一个常量的值，在编译的时候，并不需要有明确的值，但是只能为它赋值一次。也就是说可以用常量来表示这样一个值：只需要决定一次，但是需要使用很多次。但 Swift 不会自动给变量赋初始值，变量不会有默认值，所以要求使用变量之前必须要对其初始化。如果在使用变量之前不进行初始化就会报错：

```swift
var demo: String
//  note: variable defined here

let hashValue = demo.hashValue
//  error: variable 'demo' used before being initialized
```

# Optional (可选值)

## Optional 是什么？

**Optional** 其实是个 `enum`，其中有 `None` 和 `Some` 这两种类型。`nil` 就是 `Optional.None`, 非 `nil` 就是 `Optional.Some`, 通过 `Some(T)` **wrap** (包装) 原始值，这也是为什么在使用 **Optional** 的时候要 **unwrap** (解包: 从 `enum` 里取出来原始值), 同时也是 *PlayGround* 会把 **Optional** 变量显示为诸如 `{Some "hello world"}` 之类的原因，以下是 **enum Optional** 的定义：

```swift
enum Optional<T> : LogicValue, Reflectable {
  case None
  case Some(T)
  init()
  init(_ some: T)

  //  Allow use in a Boolean context.
  func getLogicValue() -> Bool

  //  Haskell's fmap, which was mis-named
  func map<U>(f: (T) -> U) -> U?
  func getMirror() -> Mirror
}
```

一个 **Optional** 变量的值是一个具体的值或者是 `nil` (表示值缺失)。在类型后加一个 `?` 来标记变量的值是可选的：

```swift
var demo: String?  //  ? 是下面这种写法的语法糖
var demo: Optional<String>
```

<center><a href = "http://uvwvu.com/syntacticSugarSwift">更多 Swift 语法糖点击此</a></center>

上面这个 **Optional** 声明的意思不是 ”声明了一个 **Optional** 的 `String` 值”, 而是 ”声明了一个 **Optional** 类型值，其中可能包含一个 `String` 值，也可能什么都不包含”。总的来说，声明的是 **Optional** 类型，而不是声明了一个 `String` 类型，这一点非常之重要。

一旦将变量声明为 **Optional** 的，如果不显式的赋值，Swift 就会给它一个默认值 `nil`。判断一个 **Optional** 变量是否有值，可以用 `if` ：

```swift
var demo: String?

if demo != nil {
  //  做些什么
}
```

## 如何使用 Optional？

在使用 **Optional** 变量的时候需要在具体的操作，比如调用方法、属性、下标索引等前面需要加上一个 `?`，如果是 `nil` 值 (`Optional.None`)，会跳过后面的操作不执行，如果有值 (`Optional.Some`)，可能会 **unwrap** ，然后对 **unwrap** 后的值执行后面的操作，来保证执行这个操作更加安全，举几个例子看看：

```swift
var demo: String?

let hashValue = demo?.hashValue
```

`demo` 是 **Optional** 类型的字符串，如果 `demo`是 `nil`，则 `hashValue` 也为 `nil`，如果 `demo` 不为 `nil`，`hashValue` 就是 `demo` 字符串的哈希值 (**Optional wrap** 之后的值)。

`?` 也可以用在 `protocol` 类型的方法上使其更加安全：

```swift
import Foundation

@objc protocol Readable {
  @objc optional func read(toPath: String) -> Bool;
}
@objc class Content: Readable {
  //  read 方法没有被实现
}

var delegate: Readable = Readable()
delegate.read?("/此处/填写/路径")
```
因为 `delegate` 是 `Readable` 类型的，其 `read` 方法是 `Optional` 的，所以它有没有实现 `read` 方法是不可确定的。**Swift** 提供了一种在参数括号前加上一个 `?` 的方式来安全地调用 `protocol` 中 `@objc optional` 方法。

**Downcast** (向下造型) 的时候也可能会用到 `as?`：

```swift
if let demoDataSource = object as? UITableViewDataSource {
  let demoRowsInSection  = demoDataSource.tableView(tableView, numberOfRowsInSection: 0)
}
```

目前为止，一共列举了四种使用场景：

1. 声明 **Optional** 变量时
2. 对 **Optional** 变量的值操作时
3. 在调用 `protocol` 的 `@objc optional` 方法时
4. **Downcast** (向下造型) 时

不过，对于 **Optional** 变量不能直接进行操作：

```swift
var demo: String?

let hashValue = demo.hashValue
//  error: value of optional type 'String?' not unwrapped; did you mean to use '!' or '?'?
```

**Optional** 变量需要 **unwrap** 后才能得到它的值，然后才能对其操作，那么如何进行 **unwarp** 呢？**unwrap** 又几种方法，一种是 **Optional Binding**：

```swift
var demo: String?

if let tmp = demo {
  let hashValue = tmp.hashValue
}
```

还有一种是在具体的操作前加上一个 `!`。

`demo` 是 **Optional** 的 `String`：

```swift
var demo: String?

let hashValue = demo!.hashValue
```

下面的 `!` 表示：“确定这里的 `demo` 一定是非 `nil` 的。”：

```swift
var demo: String?

if demo != nil {
  let hashValue = demo!.hashValue
}
```

大括号里的 `demo` 一定是非 `nil` 的，所以可以直接加上 `!` 进行 **unwrap** 并执行后面的操作。若不加判断，`demo` 又恰恰刚好是 `nil` 的，程序就会崩溃掉。

有这么一种情况：现在有一个用户定义的 `demoViewController` 类，其中有一项属性 `demoButton`，`demoButton` 是在 `viewDidLoad` 中初始化的。由于是在 `viewDidLoad` 中初始化的，所以不能直接声明为简单值：“`var demoButton: UIButton`”。之所以这样是因为非 **Optional** 的变量必须在声明时或者构造器中进行初始化，如果执意要让其在 `viewDidLoad` 中初始化，那么就要声明成：“`Optional: var demoButton: UIButton?`”。虽然可以百分百确定会在 `viewDidLoad` 中会初始化，并且在 `ViewController` 的生命周期内不会为 `nil`，但是在对 `demoButton` 操作时，每次依然要加上 `!` 来 unwrap，如果是读取值的话，也可以用 `?`：

```swift
demoButton!.frame = CGRect(x: 10, y: 10, width: 10, height: 10)
demoButton!.setTitle("demo", for: .normal)
```

对于这种类型的值，应该这样声明：“`var myLabel: UILabel!`”。这种特殊的 **Optional**，称之为 **Implicitly Unwrapped Optionals** (隐式拆包的可选值)，就等于说每次对这种类型的值操作时，都会自动在操作前补上一个 `!` 进行 **unwrap**，然后再执行后面的操作，当然如果该值是 `nil`，程序也一样会崩溃掉。

```swift
var demoButton: UIButton!  //  ! 相当于下面这种写法的语法糖
var demoButton: ImplicitlyUnwrappedOptional<UIButton>
```
那么 `!` 也讨论了两种使用场景：

1. 强制对 **Optional** 变量进行 **unwrap** 时
2. 声明 **Implicitly Unwrapped Optionals** 变量时

