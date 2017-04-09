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

完成后，你自己的待办事项列表应用程序，**Checklists** 将会如下所示：

<div align="center"><img alt="完成的 Checklists 应用程序" src="http://imgur.com/36bdaK8.png"/></div><center>完成的 Checklists 应用程序</center>

<br>

该应用程序可让你将待办事项组织到列表中，然后在完成这些项目后检查这些项目。你还可以在待办事项上设置提醒，即使应用程序未运行，iPhone 将在达到预设时间后弹出 alert。

对于待办事项列表应用程序来说，**Checklists** 是非常基本的，但不要小看它。即使这样一个简单的应用程序也已经有五种不同的屏幕和很多 scenes（场景）背后的复杂性。

##Table views 和 navigation controllers

本教程将向你介绍 iOS 应用程序中最常用的两个 UI（用户界面）元素：table view 和 navigation controller。

一个 **table view** 显示了一些事物列表。以上三个屏幕都使用 table view。事实上，这个应用程序的所有屏幕都是用 table views 制作的。这个组件非常多才多艺，而且是 iOS 开发中最重要的组件。

Navigation controller 允许你构建从一个屏幕到另一个的屏幕层次结构。它在顶部添加了一个导航栏，标题和 “back”（后退）button。

在这个应用程序中，点击列表的名称 - 例如 “Groceries” - 在包含该列表中待办事项的屏幕中滑动。左上角的 button 可让你回到上一个屏幕，并带有平滑的动画。在这些屏幕之间移动是 navigation controller 的工作。

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

##Checklists 应用程序设计

在这部分你只需要知道你在做什么，这里是一个概述有关 Checklists 应用程序的工作原理：

<div align="center"><img alt="Checklists 应用程序的所有屏幕" src="http://imgur.com/t5rRjEg.png"/></div><center>Checklists 应用程序的所有屏幕</center>

<br>

该应用程序的主屏幕显示所有的 “checklists”（1）。你可以创建多个列表来组织待办事项。

Checklists 中有一个名称，一个图标和零个或多个待办事项。你可以在 Add/Edit（添加/编辑）Checklists 屏幕（2）和（3）中编辑 Checklists 的名称和图标。

你可以点击 Checklists 的名称查看其待办事项（4）。

待办事项有描述，将项目标记为已完成的复选标记以及可选的到期日。你可以在 Add/Edit 项目屏幕（5）中编辑项目。

即使该应用没有运行，iOS 也会自动通知用户有 “remind me”（提醒我）选项集（6）的 Checklists 项目（7）。这是一个非常先进的功能，但我认为你会完成任务。

你可以在本教程的资源文件夹中找到此应用程序的完整源代码，以便与其一起玩，以了解其工作原理。

玩够了吗？然后让我们开始吧！

<code class="highlighter-rouge"><strong>重要提示：</strong>iOS Apprentice 教程仅适用于 Xcode 8.0 和更高版本。如果你仍在使用 Xcode 7，请从 Mac App Store 更新到最新版本的 Xcode。

但也不要太激进 - 通常苹果公司可以提供即将推出的 Xcode 版本的测试版本。请不要使用Xcode测试版来关注本教程。通常 beta 版本以意想不到的方式突破事件（译者注：就像 iPhone 突然没了耳机孔），你只会最终感到困惑。坚持正式版本！</code>

#与 table views 一起玩耍

看到 table views 是如此重要，你将从开始考察它们的工作原理。制作列表从来没有这么好玩过！

因为聪明的开发人员总是会将工作分解成小而简单的步骤，这是你将在第一部分中做的：

1. 在应用程序的屏幕上放置一个 table view
2. 将数据放入该 table view
3. 允许用户点击表中的一行来打开和关闭复选标记

完成这些基础知识后，你将不断在本教程中添加新功能，直到完成应用程序。

➤ 启动 Xcode 并启动新项目。选择 **Single View Application** 模板：

<div align="center"><img alt="选择 Xcode 模板" src="http://imgur.com/AyQCfve.png"/></div><center>选择 Xcode 模板</center>

<br>

Xcode 将要求你填写以下几个选项：

<div align="center"><img alt="选择模板选项" src="http://imgur.com/r6U46Ly.png"/></div><center>选择模板选项</center>

<br>

➤ 填写以下选项：

- Product Name: **Checklists**

- Team: 只需将其保留到默认设置

- Organization Name: 你的姓名或公司名称

- Organization Identifier: 在此使用你自己的标识符，使用反向域名符号

- Language: **Swift**

- Devices: iPhone

- Use Core Data, Include Unit Tests, Include UI Tests: 这些应该关闭。

➤ 按 **Next** 并选择项目的位置。

如果你愿意，你可以运行应用程序，但在这一时刻它只是一个白色的屏幕。

Checklists 只能以 portrait 方向运行，但 Xcode 刚刚生成的项目也包括 landscape。

➤ 单击 project navigator 顶部的 Checklists 项目项，然后转到 **General** 选项卡。在 **Deployment Info**，**Device Orientation** 下，确保只选择 **Portrait**。

<div align="center"><img alt="设备方向设置" src="http://imgur.com/Kq3cGhM.png"/></div><center>设备方向设置</center>

<br>

禁用 landscape 选项后，旋转设备将不再有任何影响。该应用程序始终保持 portrait 方向。

<code class="highlighter-rouge"><strong>Upside down</strong></code>

`还有一个 Upside Down（颠倒）的方向，但你通常不会使用它。`

`如果你的应用程序支持颠倒功能，用户可以旋转其 iPhone，使主屏幕位于屏幕顶部而不是底部。`

`这可能会令人困惑，特别是当用户接听电话时：麦克风是错误的，手机颠倒了。`

`另一方面，iPad 应用程序应该支持所有四个方面，包括倒置。`

## 编辑 storyboard

Xcode 创建了一个由单个 view controller 组成的基本应用程序。回想一下，view controller 表示你的应用程序的一个屏幕，并由 **Main.storyboard** 中的源代码文件 **ViewController.swift** 和用户界面设计组成。

Storyboard 包含单个文档中所有应用程序 view controller 的设计，箭头显示它们之间的流。在 storyboard 术语中，每个 view controller 被命名为*场景*。

你已经在 Bull's Eye 中使用了一个 storyboard，但在本教程中，你将解锁 storyboard 的全部功能。

➤ 单击 **Main.storyboard** 以打开 Interface Builder。

<div align="center"><img alt="设该 storyboard 编辑器与应用程序的唯一场景" src="http://imgur.com/9OANMtl.png"/></div><center>该 storyboard 编辑器与应用程序的唯一场景</center>

<br>

场景中有 iPhone 6 和 iPhone 7 的尺寸。我使用底部的 **View as:** 面板切换到较小的 iPhone SE，因为占用的空间较小。然而，你选择编辑 storyboard 的设备大小无关紧要：应用程序将自动调整大小以适应所有 iPhone 型号。

➤ 在左侧的轮廓窗格中选择 **View Controller**。

提示：回想一下，大纲窗格显示故事板中所有场景的视图层次结构。如果看不到大纲窗格，请单击“界面构建器”窗口底部的小箭头按钮来切换其可见性。

<div align="center"><img alt="此按钮显示并隐藏轮廓窗格" src="http://imgur.com/s7R5Nyw.png"/></div><center>此按钮显示并隐藏轮廓窗格</center>

<br>

➤ 按键盘上的 **delete** 从 storyboard 中删除 **View Controller Scene**。画布应为空，大纲窗格显示 “No Scenes”（无场景）。

你正在删除此场景，因为你不需要常规 view controller，而是要使用所谓的 **table view controller**。这是一种特殊类型的 view controller，它使得使用 table views 更容易一些。

要将 ViewController 的类型更改为 table view controller，你首先必须编辑其 Swift 文件。

➤ 单击 **ViewController.swift**，在源代码编辑器中打开它，并从下面更改以下行：

```swift
class ViewController: UIViewController {
```

到这里：

```swift
class ChecklistViewController: UITableViewController {
```

通过此更改，你可以告诉 Swift 编译器，你自己的 view controller 现在是一个 UITableViewController object，而不是常规的 UIViewController。

记住，从 “UI” 开始的一切都是 UIKit 的一部分。这些预制组件可以作为你自己的应用程序的构建块。

当 Xcode 创建项目时，它假设你希望将 ViewController object 构建在基本的 UIViewController 之上，但是在这里，你正在将其更改为使用 UITableViewController 构建块。

你还将 ViewController 重命名为 ChecklistViewController 以给它一个更具描述性的名称。这是你自己的 object - 你可以告诉它，因为它的名称不是从 UI 开始的。

在本教程的过程中，你将向 ChecklistViewController object 添加数据和 functionality，使应用程序实际执行操作。你还将向应用程序添加多个新的 view controller。

➤ 在左侧的 Project navigator 中，单击一次以选择 **ViewController.swift**，然后再次单击以编辑其名称。（不要双击太快，否则你将在新的源代码编辑器窗口中打开 Swift 文件）

将文件名更改为 **ChecklistViewController.swift**：

<div align="center"><img alt="重命名 Swift 文件" src="http://imgur.com/prH1mxU.png"/></div><center>重命名 Swift 文件</center>

<br>

你现在可能会收到警告：“The document could not be saved. The file has been changed by another application.”（该文档无法保存。该文件已被其他应用程序更改。）单击 **Save Anyway 以使其消失。

➤ 返回 storyboard，将 **Table View Controller** 从 Object Library（右下角）拖动到画布中：

<div align="center"><img alt="将 Table View Controller 拖动到 storyboard 中" src="http://imgur.com/b4nZ3GN.png"/></div><center>将 Table View Controller 拖动到 storyboard 中</center>

<br>

这将添加一个新的 Table View Controller 场景到 storyboard。

➤ 转到 **Identity inspector**（Xcode 窗口右侧的检查器窗格中的第三个选项卡）以及 **Custom Class** 分类下面的 **ChecklistViewController**（或使用小箭头选择它）。

提示：执行此操作时，请确保选择了实际的 Table View Controller，而不是其中的 Table View。场景周围应该有一个淡蓝色的边框。

<div align="center"><img alt="更改 Table View Controller 的 Custom Class" src="http://imgur.com/6ROUvXg.png"/></div><center>更改 Table View Controller 的 Custom Class</center>

<br>

左侧轮廓窗格中的场景名称应更改为 “Checklist View Controller Scene”。你已成功将ChecklistViewController 从常规 view controller object 更改为view controller object。

顾名思义，你可以在 storyboard 中看到，view controller 包含一个 Table View object。我们将尽快介绍 controllers 和 views 之间的区别，但是现在记住，controller 是整个屏幕，而 table view 是实际绘制列表的 object。

如果没有大箭头指向新的 table view controller，则转到 **Attributes inspector**，然后将 **Is Initial View Controller** 打上勾。

<div align="center"><img alt="更箭头指向 initial view controller（初始视图控制器）" src="http://imgur.com/SMRnNvi.png"/></div><center>箭头指向 initial view controller（初始视图控制器）</center>

<br>

Initial view controller 是你的用户将看到的第一个屏幕。如果没有它，iOS 应用程序启动时，不会知道让哪个 view controller 从你的 storyboard 中加载，你将最终盯着黑屏。

➤ 在 Simulator 上运行应用程序。

你应该看到一个空的列表。这是 table view。你可以上下拖动列表，但它不包含任何数据。

<div align="center"><img alt="该应用程序现在使用一个 table view controller" src="http://imgur.com/XskeEOu.png"/></div><center>该应用程序现在使用一个 table view controller</center>

<br>

顺便说一下，使用哪个 Simulator 并不重要。Table views 可以自动调整设备的尺寸，并且该应用程序在小型 iPhone SE 和巨大的 iPhone 7 Plus 上表现也同样出色。

就我个人而言，我使用的是 iPhone SE Simulator，因为它适合我的 Mac 的屏幕，只是勉强！（请记住，你可以使用 **⌘1**，**⌘2** 和 **⌘3** 缩放 Simulator 窗口）

<code class="highlighter-rouge"><strong>注意：</strong>构建应用程序时，Xcode 会发出警告：“Prototype cells must have reuse identifiers”（原型单元必须具有重用标识符）。现在不要担心，我们会尽快解决这个问题。</code>

##剖析 table view

首先，让我们再来谈一谈 table views。UITableView object 显示一些事物列表。

<code class="highlighter-rouge"><strong>注意：</strong>我不知道为什么它被命名为 *table*（表），因为表通常被认为是具有多行和多列的 spreadsheet-type（电子表格类型）的 object，而 UITableView 只有行。它和表比起来更像是一个列表，但是我想我们现在不要再纠结命名了。UIKit 还提供了一个 UICollectionView object 它类似于 UITableView 但允许多列。</code>

有两种样式的表：“plain” 和 “grouped”。他们的工作主要是相同的，但有一些小的差异。最明显的不同之处在于，grouped 样式的表中的行将放置在浅灰色背景的框（groups）中。

<div align="center"><img alt="Plain 样式的表（左）和 grouped 样式的表（右）" src="http://imgur.com/yzSLeD8.png"/></div><center>Plain 样式的表（左）和 grouped 样式的表（右）</center>

<br>

Plain 样式用于所有表示类似东西的行，例如地址簿中的每个行包含一个人的名称的联系人。

当每行代表不同的东西，例如其中一个联系人的各种属性时，使用 grouped 样式。Grouped 样式的表将具有名称行，地址行，电话号码行等。

你将在 Checklists 应用程序中使用两种样式的表。

表格的数据以**行**的形式出现。在第一个版本的 Checklists 中，每一行将对应一个待办事项，你可以在完成之后检查。

尽管不推荐使用这种设计，但你可能会有许多行（数万）。大多数用户会有一个令人难以置信的烦恼，就是滚动一万行找到来他们想要的那行，谁可以责怪他们...

表格中的数据显示在 **cells**（单元格）中。一个单元格与一行相关，但它不完全相同。单元格是一个视图，显示在该时刻恰好可见的一行数据。如果你的表格可以在屏幕上一次显示10行，那么它只有 10 个单元格，即使可能有数百行的实际数据。

每当一行滚动屏幕并变为不可见时，其单元格将重新用于滚动到屏幕的新行。

<div align="center"><img alt="单元格显示行的内容" src="http://imgur.com/nziYhDP.png"/></div><center>单元格显示行的内容</center>

<br>

