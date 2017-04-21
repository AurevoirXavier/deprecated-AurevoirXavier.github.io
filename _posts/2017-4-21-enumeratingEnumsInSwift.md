---
layout: post
title: "Enumerating enums in Swift"
date:   2017-04-21
excerpt: "遍历 Swift 中的枚举类型"
tags: [enums, program, swift]
comments: true
---

我天真地定义了以下枚举：

```swift
enum Letter: String {
    case A = "a", B = "b", C = "c"
}
```

定义完后我大概可以做一些类似这样的事情：

```swift
for element in Letter.allValues {
  //Do something for each element
}
```

不… 这不起任何作用。