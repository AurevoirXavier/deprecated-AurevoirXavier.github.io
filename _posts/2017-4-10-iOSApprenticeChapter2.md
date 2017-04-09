---
layout: post
title: "iOS Apprentice 1 Getting Started v5.0 Chapter 2"
date:   2017-04-10
excerpt: "翻译中"
tags: [program, iOS, translate]
comments: true
---

`Tips：专有名词我只会在它第一次出现时翻译，后续不再翻译。`

- `毕竟你要和全英文的 IDE（集成开发环境）打交道，译后你甚至可能找不到它在何处。`
- `当你以后进入公司，保留着这种习惯一定会影响你与同事的交流。`
- `上网翻阅资料或询问他人时，无论哪里对于专有名词都是直接引用。`

一般译作中很少出现英文，不过为了帮助你尽快融入其中，我会在翻译一次之后直接给出。可能一开始你会不习惯，这些中文中穿插着英文，但这些关键词至关重要，特别是在面向对象编程中。如果你在这里学会了，它将不仅仅适用于 Swift，在你整个编程生涯中它们都占据着绝对地位。一个优秀的程序员是会经常阅读别人的代码来学习并提升自己，社区，[GitHub](https://www.github.com/)，[Stack Overflow](https://stackoverflow.com/) 等地方都是牛人聚集地。你可以在其中看到不少杰出的作品，并且不少人以回答问题解决困难为乐，不过这些网站对你的英文水平有着不小的考验。最后，我列出了一个[清单](http://uvwvu.com/iOSkeyword)，里面包含了本书涉及到的所有专有名词，希望能够帮助你适应。

---

<br>

<h1 align="center">iOS Apprentice 第二章</h1>

<center><strong>Aurevoir Xavier 译</strong></center>

<br>

#你自己的待办事项应用程序

待办事项列表应用程序是 App Store 中最受欢迎的应用程序之一，仅次于无聊的应用程序。iPhone 甚至配有 Reminders 应用程序（但幸运的是没有内置无聊的应用程序）。

制作一个待办事项列表应用程序有点像一个流行的 iOS 开发人员的通行证，必经之路，所以你也有道理创建一个。

完成后，你自己的待办事项列表应用程序，清单将会如下所示：

<div align="center"><img alt="完成的清单应用程序" src="http://imgur.com/36bdaK8.png"/></div><center>完成的清单应用程序</center>

<br>

该应用程序可让你将待办事项组织到列表中，然后在完成这些项目后检查这些项目。你还可以在待办事项上设置提醒，即使应用程序未运行，iPhone 将在达到预设时间后弹出 alert。

对于待办事项列表应用程序来说，**清单** 是非常基本的，但不要小看它。即使这样一个简单的应用程序也已经有五种不同的屏幕和很多 scenes 背后的复杂性。

##Table views 和 navigation controllers

本教程将向你介绍 iOS 应用程序中最常用的两个 UI（用户界面）元素：table view 和 navigation controller。

一个 **table view** 显示了一些事物列表。以上三个屏幕都使用 table view。事实上，这个应用程序的所有屏幕都是用 table views 制作的。这个组件非常多才多艺，而且是 iOS 开发中最重要的组件。

Navigation controller 允许你构建从一个屏幕到另一个的屏幕层次结构。它在顶部添加了一个导航栏，标题和 “back”（后退）button。

在这个应用程序中，点击列表的名称 - 例如 “Groceries” - 在包含该列表中待办事项的屏幕中滑动。 左上角的 button 可让你回到上一个屏幕，并带有平滑的动画。在这些屏幕之间移动是 navigation controller 的工作。

Navigation controllers 和 table views 通常一起使用：

<div align="center"><img alt="顶部的灰色栏是导航栏。项目列表是 table view。" src="http://imgur.com/RenMs3z.png"/></div><center>顶部的灰色栏是导航栏。项目列表是 table view。</center>

<br>

看看你的 iPhone 附带的应用程序 - 日历，消息，笔记，联系人，邮件，设置 - 你会注意到即使它们看起来稍有不同，所有这些应用程序的工作方式几乎相同。

这是因为它们都使用 table views 和 navigation controllers：

<div align="center"><img alt="这些都是 navigation controllers 内的 table views" src="http://imgur.com/ZdiLvJf.png"/></div><center>这些都是 navigation controllers 内的 table views</center>

<br>

（音乐应用程序的底部还有一个标签栏，你将在下一个教程中了解一些相关内容）

如果你想了解如何编程 iOS 应用程序，则需要掌握这两个组件，因为它们几乎在每个应用程序中都可以出现。这正是你在本教程中的重点。你还将学习如何将数据从一个屏幕传递到另一个屏幕，这是一个非常重要的主题，常常让初学者迷惑不解。

完成本课后，**view controller**，**table view** 和 **delegate** 的概念将非常熟悉，你可以在睡眠中编程（尽管我希望你能梦想其他的事情）。

这是一个非常长的阅读与大量的源代码，所以花时间让它全部沉积下来。我鼓励你去体验一下你将要写的代码。更改其内容，看看它的作用，即使会破坏应用程序。

导致 bugs 的错误，沮丧的撕裂头发，发现错误的光辉时刻，修复错误的成就感 - 它们是学习过程的所有重要部分。

毫无疑问，玩代码是最快的学习方式！

顺便说一句，如果你不清楚某些东西 - 例如，你可能会想知道为什么 Swift中 的方法名称看起来很有趣 - 那么不要惊慌！保持一些信念，继续前进...一切都会在适当的时候给予解释。

##清单应用程序设计

在这部分你只需要知道你在做什么，这里是一个概述有关清单应用程序的工作原理：

<div align="center"><img alt="清单应用程序的所有屏幕" src="http://imgur.com/t5rRjEg.png"/></div><center>清单应用程序的所有屏幕</center>

<br>

该应用程序的主屏幕显示所有的 “checklists”（清单）（1）。你可以创建多个列表来组织待办事项。

清单中有一个名称，一个图标和零个或多个待办事项。你可以在 Add/Edit（添加/编辑）清单屏幕（2）和（3）中编辑清单的名称和图标。

你可以点击清单的名称查看其待办事项（4）。

待办事项有描述，将项目标记为已完成的复选标记以及可选的到期日。你可以在 Add/Edit 项目屏幕（5）中编辑项目。

即使该应用没有运行，iOS 也会自动通知用户有 “remind me”（提醒我）选项集（6）的清单项目（7）。这是一个非常先进的功能，但我认为你会完成任务。

你可以在本教程的资源文件夹中找到此应用程序的完整源代码，以便与其一起玩，以了解其工作原理。

玩够了吗？然后让我们开始吧！

