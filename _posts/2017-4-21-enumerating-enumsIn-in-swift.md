---
layout: post
title: "Enumerating enums in Swift"
date:   2017-04-21
excerpt: "遍历 Swift 中的枚举类型"
tags: [Swift]
comments: true
---

<center><h1>我天真地定义了以下枚举：</h1></center>

<!--more-->

我天真地定义了以下枚举：

```swift
enum Letter: String {
    case A = "a", B = "b", C = "c"
}
```

定义完后我大概可以做一些类似这样的事情：

```swift
for element in Letter.allValues {
	//	Do something for each element
}
```

不… 这不起任何作用。枚举是一些超类中根据上下文有效值的子集 (Swift 实际上采取了一种更聪明的方式，但我认为在此处无关紧要)，当然你可能希望迭代所有有效的值。

那么为什么没有默认的迭代器？我认为这是因为一个枚举应该被认为是一个集合，所以 Swift 无法知道什么是正确的顺序。字母表？数值由高到低？其他语言可能已经空出未定义行为，不做定义，让你自己决定 (你将以任何顺序获取值，不依赖于它)，但这很不 Swift (清真)。所以我认为苹果已经留给了让我们自己定义空间，如果我们有需要的话。

这告诉我，我应该使用以下模式：

```swift
enum Letter: String {
    case A = "a", B = "b", C = "c"
    
    static let allValues = [A, B, C]
}
  
for element in Letter.allValues {
	//	Do something for each element
}
```

在这里我们定义了枚举的顺序，我想我们甚至可以提供多个顺序 (如果这些值实际上是键入本地化的字符串，那么甚至可以响应语言环境，然后我们想根据语言环境进行排序)。

有一个问题... 我们如何确定所有的值都包含所有可能的值？悲剧的是，我找不到可以解决这个问题的方法。如果不是真正强大的解决方案，那么一个单元测试通过检查存储在 allValues 的每个值中至少可以给你自己上一个双重保险。

我很乐意听到有关这个话题的其他想法，请发表评论。