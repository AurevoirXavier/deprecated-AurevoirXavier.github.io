---
layout: post
title: "atomically"
date:   2017-04-11
excerpt: "atomically 参数详解"
tags: [program, swift]
comments: true
---

## atomically 通常用在哪？

很多人都会有这个问题：**writeToFile: atomically:** 这个方法 (比如 - [NSArray writeToFile: **atomically:**]) 中的 **atomically:** 参数代表什么。

举个更生动的例子吧：

```swift
func dataFilePath() -> URL { 
  return documentsDirectory().appendingPathComponent("Checklists.plist")
}

func saveChecklists() {
  let data = NSMutableData() 
  let archiver = NSKeyedArchiver(forWritingWith: data)

  archiver.encode(lists, forKey: "Checklists")
  archiver.finishEncoding()
  data.write(to: dataFilePath(), atomically: true)
}
```

上面的代码是用来储存信息到一个名为 **Checklist.plist** 的文件里。

我们通常传递给 **atomically:** 一个 **true** 或 **YES**，但却不知道这是什么意思。

## atomically 是什么？

**atomically** 叫 “原子写入” 或者说 “文件的写入原子性” 是用来保护对文件进行正确且完整的写入。当正在写入时，不好的事情（停电，驱动器崩溃之类的）发生了，这就导致文件写入了一部分另外一部分没有写入，这通常不是你想要的。

## 如何使用 atomically？

如果 **true** 或 **YES**，则将数据写入一个临时备份文件。假设没有发生错误，程序会将备份文件重命名为由路径指定的名称（等同于替换掉目标文件），如果发生错误的话，那也只是发生在那个临时备份文件上，真正的目标文件不会受影响；否则，数据直接写入路径指定的目标文件。