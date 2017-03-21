---
layout: post
title: "iOS Apprentice 1 Getting Started v5.0 （译）"
date:   2017-03-21
excerpt: "译至 120 页"
tags: [program, iOS, translate]
comments: true
---

`Tips：专有名词我只会在它第一次出现时翻译，后续不再翻译。`

- `毕竟你要和全英文的 IDE（集成开发环境）打交道，译后你甚至可能找不到它在 IDE 的何处。`
- `当你以后进入公司，保留着这种习惯一定会影响你与同事的交流。`
- `上网翻阅资料或询问他人时，无论哪里对于专有名词都是直接引用。`

可能一开始你会不习惯，这些中文中穿插着英文，但是这些关键词是至关重要的，特别是在面向对象语言中。如果你在这里学会了，它将不仅仅适用于 swift，在你整个编程生涯中它们的身影随处可见。下面我会列出一个 List（清单） 帮助你适应一下。

<center><strong>iOS 开发专有名词</strong></center>

<br>

<center><strong>表一</strong></center>

<center><strong>

Storyboard 故事版		Interface Builder 界面构造器

<br>

Table views 表视图		Navigation controller 导航控制器

</strong></center>

| Storyboard                  | 故事板          |      | Interface Builder          | 界面构造器      |
| :-------------------------- | :----------- | :--: | :------------------------- | :--------- |
| **Table views**             | **表视图**      |      | **Navigation controllers** | **导航控制器**  |
| **Delegates**               | **代理**       |      | **Core Location**          | **核心位置**   |
| **Core Data**               | **核心数据**     |      | **Map Kit**                | **地图工具包**  |
| **Single View Application** | **单一视图应用程序** |      | **Navigator Area**         | **导航区域**   |
| **Project Navigator**       | **项目导航器**    |      | **Utilities pane**         | **实用程序窗格** |
| **View controller**         | **视图控制器**    |      | **Scene**                  | **场景**     |
| **Object Library**          | **对象库**      |      | **Controls**               | **控件**     |
| **Outline pane**            | **大纲窗格**     |      | **Connections inspector**  | **连接检查器**  |
| **Issue navigator**         | **问题导航器**    |      | **Portrait**               | **竖屏**     |

<br>

<center><strong>表二</strong></center>

| Landscape                | 横屏        |      | **Orientation** | 方向     |
| :----------------------- | :-------- | :--- | :-------------- | :----- |
| **Attributes inspector** | **属性检查器** |      | **View**        | **视图** |
| **Closure**              | **闭包**    |      | **Simulate**    | **模拟** |

<br>

<center><strong>软件开发专有名词</strong></center>

<br>

<center><strong>表一</strong></center>

| SDK Software Development Kit | 软件开发工具包   |      | Variable          | 变量       |
| :--------------------------- | :-------- | :--- | :---------------- | :------- |
| **Object**                   | **对象**    |      | **Method**        | **方法**   |
| **Object-oriented**          | **面向对象**  |      | **Slider**        | **滑块**   |
| **Button**                   | **按钮**    |      | **Alert**         | **提醒**   |
| **Labels**                   | **标签**    |      | **Canvas**        | **画布**   |
| **Action**                   | **操作；动作** |      | **Frameworks**    | **框架**   |
| **UI**                       | **用户界面**  |      | **Data**          | **数据**   |
| **Function**                 | **函数**    |      | **Functionality** | **功能**   |
| **Type**                     | **类型**    |      | **Debug**         | **调试**   |
| **String**                   | **字符串**   |      | **Data types**    | **数据类型** |

<br>

<center><strong>表二</strong></center>

| Assignment     | 赋值     |      | Bug                   | 漏洞       |
| :------------- | :----- | :--: | :-------------------- | :------- |
| **Global**     | **全局** |      | **Instance**          | **实例**   |
| **Local**      | **本地** |      | **Instance variable** | **实例变量** |
| **Algorithm**  | **算法** |      | **Constant**          | **常量**   |
| **Width**      | **宽度** |      | **Height**            | **高度**   |
| **Background** | **背景** |      | **Color**             | **颜色**   |

---

<br>

<h1 align="center">iOS Apprentice 第一章</h1>

<center><strong>Aurevoir Xavier 译</strong></center>

<br>

嗨！我是 Matthijs Hollemans，一名全职 iOS 开发人员和 [www.raywenderlich.com](www.raywenderlich.com) 的辅导团队成员。

接下来你将要读第一章导读部分来自我的书 *iOS Apprentice: Beginning iOS Development with Swift, Fifth Edition* 。

在本书中，你将学习如何使用苹果的 Swift 3.0 编程语言，并通过这一系列的四个史诗级长度的动手教程来制作自己的 iPhone 和 iPad 应用程序。

<div align="center"><img alt="你将在 iOS Apprentice 中制作的应用程序" src="http://i.imgur.com/AwL2UfX.png"/></div><center>你将在 iOS Apprentice 中制作的应用程序</center>  

<br>

每个人都喜欢游戏，所以你将会以打造一个简单而有趣名字叫 Bull's Eye 的 iPhone游戏作为开始。他会教会你 iPhone 编程的基础知识，其他的教程将会建立在这个基础之上。

最好的地方就是你可以在这里免费享受完整的阅读！

本书中的每一个教程都描述了一个新的应用程序的所有细节，同时它们涵盖了在你制作你的 App 的过程中所需要知道的一切。在这一系列结束之际，你会有足够的经验把你的想法变成真正的应用程序，然后你可以把它放在 App Store 上！

即使你以前从未编过程，或者你是 iOS 新手，你也应该能够按照一步一步的说明来操作，并了解这些应用是如何制作出来的。每个教程都有大量的图片以防止你迷失方向。虽然不是一切都可能有意义，但它们就挂在那里，可以让思路全程都显得清晰。

编写自己的 iPhone 和 iPad 应用程序是一个很多乐趣，但同时又有许多辛苦工作的过程。如果你有想象力和毅力，那么一切都不是问题。我真诚地相信，这个系列可以将你从一个彻彻底底的新手打造成一个成熟的 iOS 开发人员，但你必须投入时间和精力。通过写这些教程我已经完成了我的部分，那么现在交给你了！（师父领进门，修行在个人）

享受第一个教程吧！如果它对你有用，那么我希望你从 [www.raywenderlich.com/store/ios-apprentice](www.raywenderlich.com/store/ios-apprentice) 或亚马逊来获得它的其余部分。

## 关于这本书

这部 iOS Apprentice 将帮助你成为一个杰出的 iOS 开发人员，但主要还是取决于你是否用好它。这里有一些提示，将帮助你充分利用这本书。

#### 通过重复学习

你会通过这本书做很多应用程序。即使这些应用程序开始时相当简单，你可能会觉得教程有些繁琐难以遵循，特别是你从来没有做过任何计算机编程——因为我会介绍很多新的概念。

如果你没有立刻理解一切，没有关系，只要你得到一个一般的笼统的概念或想法。在本系列的后续教程中，我们将再次讨论这些概念，直到它们刻在你的心里。

#### 遵循说明靠自己

重点说的是，你不只是阅读说明，而且事实上你还要**遵循**他们。打开 Xcode，输入源代码片段，并在模拟器中运行应用程序。这有助于你了解应用程序是如何逐步构建出来的。

更好的是，与代码作乐。随意修改应用程序的任何部分，看看结果是什么。实验和学习！不要担心弄坏它们，这是一半的乐趣所在。你总是可以找到回到开始的方法。

#### 不要惊慌——错误发生！

你将会遇到问题，这点我可以打包票。你的程序可能会有奇怪的错误，并将让你陷入困境。相信我，我已经从事编程 30 年了，这些仍发生在我的身上。我们都只是人类，我们的大脑都只能处理一定复杂程度的编程问题。在这个课程中，我会给你工具，你心灵的工具箱，它会帮助你找到你自己不小心挖出的坑。

#### 了解复制粘贴的节拍

有非常多的人试图通过盲目地复制粘贴在博客和其他网站上发现的代码来编写 iPhone 应用程序，却不知道其中代码的真正作用，以及该如何适配它们的程序。

在网上寻找解决方案这一行为并没有什么错——我一直都这样——但我想给你工具和知识然后让你去了解你在做什么，以及为什么。

这是实践的练习建议，并不只是一堆干巴巴的理论（虽然不可避免的会涉及一些理论）。你将从刚开始入门就构建真正的应用程序，我将解释一切是靠着什么方式来运作，并且有大量的图片来辅助说明到底发生了什么。

我会尽我所能地讲清楚一切是如何相互配合的，为什么我们要以某种方式去做事情，以及替代方案会有哪些。

#### 做练习

我将会了解一下，对于某些事你的想法是怎样的——是的，这里有一些练习！事实上，做这些练习能最大程度地激发你的想法。知道路怎么走和怎么走这条路之间有着巨大差别，而学习编程的唯一方法就是做到这一点。我鼓励你不只是做练习，而且要玩玩那些你将要写的代码（比如说修改几处看看会有何变化，或者加一些自己的功能）。实验，改进，尝试添加新功能。软件是一个复杂的机械，要找出它的工作原理，有时你必须在轮子上放一些辐条，把整件事情分开。这就是你的学习方式！

#### 尽情享受

最后但并不是最重要的，记得享受其中！一步一步建立起你的编程理解，同时开发出有趣的应用程序。在本系列的结尾，你会学到 Swift 和 iOS 开发包的基本要素。更重要的是，你应该有一个很好的想法关于如何将一切结合在一起，如何像一个程序员一样去思考问题。

这是我的目标，在这些教程之后，你将学到能使你成为一个足以站得住脚的开发人员的知识。我相信，只要你把这些基础知识拿下，你将能够编写任何你想要的 iOS 应用程序。你还有很多东西要学习，但当你通过 *iOS Apprentice* 这本书，你便可以独立地放手去做。

## 本书写给哪些人

这本书最棒的地方就是，无论你是全新的编程菜鸟，或者是有着其他编程背景的程序员，并且期待去学习 iOS 开发，都非常适合。

如果你是一个彻头彻尾的开发新手，不要担心——这本书并没有假设你有任何有关编程或制作应用程序的基础。当然，如果你有编程经验，那么会有助于你更快上手。Swift 是一种新兴的编程语言，但在许多方面与 PHP，C#，Javascript 之类的流行语言有着相似之处。

如果你曾使用过 iOS 的 Object-C 开发语言，那么它低水平的特性和奇怪的语法可能会让你失望。好吧，这里有一个好消息告诉你：现在，通过 Swift 我们拥有了更现代化的语言，iOS 开发相对过去已经变得容易了很多。

教会你一切 iPhone 和 iPad 的开发知识不是本系列的目的。因为 iOS SDK（软件开发工具包）实在是太庞大了，我们没有办法去涉及到它的一切——但幸运的是，我们并不需要了解所有。你只需要掌握 Swift 和 iOS 的基本构建块。一旦你了解了这些基本原理，你可以很容易的通过自己来找出它是如何工作的，并自学其余的部分。

我要教会你的最重要的一件事就是，如何像一个程序员一样思考。这将帮助你上手任何编程任务，无论是游戏，使用程序，使用 Web 服务的移动应用程序，或任何其他你可以想象到的。

作为一个程序员，你常常不得不考虑困难麻烦的计算问题，并寻找创造性的解决方案。通过有条不紊的分析问题，你最终将会解决它们，无论有多么复杂。一旦你拥有这个宝贵的技能，你可以编写出任何东西！

## 仅针对 iOS 10 或更高版本

本系列教程专门针对 iOS 10 及更高版本。每个新版本的 iOS 都是与前一个有很大的便利，继续开发旧设备和旧 iOS 版本，意义并不是很大。事情在移动计算世界中飞速发展！大多数的 iPhone，iPod 和 iPad 用户都会很快地升级到最新版本的 iOS，所以你不需要太担心潜在客户的流失。

旧版设备的拥有者（例如 iPhone 4S 或 第一代 iPad）可能会被 iOS 9 或更早版本所困扰，但这只是市场的一小部分。支持这些较旧的 iOS 版本所花费的成本远超出得到的回报。

不过最终还是由你自己决定是否让应用程序支持旧设备，但我的建议是，应该将工作的重点放在他们最重要的地方。苹果作为一个公司总是不懈地展望未来——如果你想在苹果的地盘玩耍，跟随他们的领导是个明智的选择。那么，放眼未来吧！

## 你需要些什么

为 iPhone 和 iPad 做开发，这是一个很大的乐趣，但像大多数爱好（或企业）它将花费一些物力财力。当然，一旦你掌握并灵活使用它，打造出一个出色的应用程序，你将有潜力赚回这笔钱的数倍。

#### 你必须要投入以下列出的：

**iPhone，iPad 或 iPod touch**。我假设你至少拥有其中一样。iOS 10 运行在以下设备上：iPhone 5 或更新版本，iPad 第四代或更新的版本，iPod touch 第六代。如果你有一个旧的设备，那么这是一个好时机考虑获取升级。但不要担心，如果你没有一个合适的设备：你可以在模拟器上完成你的一切操作。

<code class="highlighter-rouge"><strong>注意：</strong>尽管我在本教程中主要讨论 iPhone，但我所说的一切都适用于 iPad 和 iPod touch。除了小的硬件差异，它们使用 iOS，你完全可以按照相同的方式为它们编程。你应该还可以在 iPad 和 iPod touch 上运行本系列教程中教授的所有应用程序，并且不会出现问题。</code>

**Mac 计算机与 intel 处理器**。你在过去几年间买的任何 Mac，即使是 Mac mini 或 MacBook Air。它需要至少有
OS X 10.11 EI Capitan 或 macOS 10.12 Sierra。Xcode，iOS 应用程序的开发环境，它是一个非常吃内存的工具，所以占用你 4 GB 的内存完全不算什么。也许你不会用这么多，但是不要委屈自己，升级一下你的 Mac。RAM 越多越好。一个聪明的开发者应该会懂得在工具和设备下点成本。

有一些方法，可以让你在 Windows 或 Linux 机器上开发 iOS 应用程序，或者安装了 macOS 的 PC（所谓的 “Hackintosh” ），但是你用 Mac 的话，可以省去不少麻烦。

如果你买不起最新的机型，从而打算去 eBay 购入一个二手的 Mac。只要确保它满足最低要求（intel CPU，最好超过 1 GB RAM）。如果你碰巧买到一台装有较旧版本的 OS X（10.10 Yosemite 或更早版本）的机器，你可以从在线 Mac App Store 免费升级到最新版本的 macOS。

**Apple 开发者计划账户**。你可以免费下载所有开发工具，你可以在开发过程中在自己的 iPhone，iPad 或 iPod touch 上使用你的应用程序，因此你不必加入 Apple 开发人员计划。但要将完成的应用程序提交到 App Store，你必须注册付费开发者计划。这将花费你 $99 每年。有关详情请参见 [developer.apple.com/programs/](developer.apple.com/programs/)。

## Xcode

我们的第一个工作是下载并安装 Xcode 和 iOS SDK。

<div align="center"><img alt="" src="http://imgur.com/1flkRks.png"/></div>

Xcode 是为 iOS 应用程序量身定做的开发工具。它有一个文本编辑器，你可以在其中键入你的源代码，它还有一个可视化编辑器，用于设计你的应用程序用户界面。

Xcode 将你编写的源代码转换为可执行的应用程序，并在模拟器或 iPhone 上启动它。因为没有任何应用程序是完全没有 bug 的，所以 Xcode 还配备了一个调试器，可以帮助你发现代码中存在的缺陷（不幸的是，它并不会自动修复，这仍然是你的工作）。

你可以从 Mac App Store 免费下载 Xcode（[itunes.apple.com/app/ xcode/id497799835](itunes.apple.com/app/ xcode/id497799835)）。这至少需要 OS X EI Capitan（10.11），所以如果你仍运行 OS X Yosemite 或甚至是 Mavericks，你必须首先升级到最新版本的 macOS（也可以免费从 Mac App Store 获取）。做好下载一个大型软件的心理准备，因为一个完整的 Xcode 包大约是 5 GB。

重要事项：你的系统上可能已经有一个预装的 OS X 的 Xcode 版本。该版本绝对是已经过期的了，因此不要使用它。Apple 定期发布新版本，并且鼓励你始终使用最新版本的 OS X ，Xcode 和 SDK 来进行开发。

我在 macOS Sierra（10.12）上用 **Xcode 8.0** 和 **iOS 10.0** SDK 编写了本书的最新修订版本。当你阅读本书时，毫无疑问这个版本号肯定会再次上升。我将尽力保持 PDF 教程中使用的版本与要官方发布的最新版本保持同步，但如果我所展示的屏幕截图与你在屏幕上看到的实际内容不完全一致，不要惊慌。在大多数情况下，差异将很小。

很多较旧的书籍和博客（任何2010年之前的）谈论 Xcode 3，这与 Xcode 有着天差地别的代沟。更新的材料也许会提到 Xcode 版本 4，5，6 或 7，乍看之下，类似于 Xcode 8，但在许多细节上有所不同。所以如果你正在阅读一篇文章，你看到的 Xcode 的图片与你实际运行的 Xcode 界面不同，那么可以肯定他们讨论的是一个旧的版本。不过话说回来，你仍然可以从这些文章中获得一些东西，因为编程示例仍然有效。它们的区别只是来自于不同的爸妈（开发工具）。

## 前景：概述

*iOS Apprentice* 分为四个教程部分，从开始到其中的主题。在每个教程中，你将从头开始构建一个完整的应用程序！让我们先来看看将要做些什么。

#### 教程1：入门

在第一个教程中，你将开始建立一个名为 *Bull's Eye* 的游戏。你将学习如何以一种轻松的方式使用 Xcode，Interface Builder（界面构造器） 和 Swift。

<div align="center"><img alt="" src="http://imgur.com/TolF1G2.png"/></div>

#### 教程2：清单

在本系列的第二个教程中，你将创建自己的待办事项列表应用程序。你将了解所有 iOS 应用程序使用的基本设计模式，以及 table views（表视图），navigation controllers（导航控制器）和 delegates（代理）。现在，你即将真正的打造出一个应用程序！

<div align="center"><img alt="" src="http://imgur.com/Dm64Fp1.png"/></div>

#### 教程3：我的位置

在本系列的第三个教程中，你将开发一个位置感知的应用程序，让你创建一个保存你感兴趣的地点的列表。在此过程中，你将了解 Core Location（核心位置），Core Data（核心数据），Map Kit（地图工具包）等等！

<div align="center"><img alt="" src="http://imgur.com/hhv9qH9.png"/></div>

#### 教程4：商店搜索

移动应用程序常需要与 Web 服务交流，这就是你在本系列中的最后一个教程中将要做的。你将创建出一个时尚的应用程序，让你使用 HTTP 请求和 JSON 在 iTunes 商店搜索产品。

<div align="center"><img alt="" src="http://imgur.com/UFl2syN.png"/></div>

让我们开始吧，把你打造成一个真正的 iOS 开发者！

## 计算机的语言

iPhone 可能假装它是一个电话，但它实际上是一个非常先进的计算机，也恰巧能够打电话。

像任何计算机一样，iPhone 通过 1 和 0 来工作。当你编写在 iPhone 上运行的软件时，你不得不将你头脑中的想法转换成计算机可以理解的那些数字（译者注：二进制的 1 和 0）。

幸运的是，你不必自己写任何二进制代码。那样的要求对人类的大脑而言太苛刻了。另一方面，日常的英语不够精确到用于计算机编程。

你将使用中间语言 Swift，它有一点像英语，所以他是相当简单让我们人类理解，同时它可以很容易的翻译成计算机可以理解的东西。

这是计算机说的语言：

<div align="center"><img alt="" src="http://imgur.com/iPEEMm6.png"/></div>

<center>译者注：上图为汇编层面上的代码。</center>  

<br>

事实上，在计算机眼中是这样的：

<div align="center"><img alt="" src="http://imgur.com/718hXkS.png"/></div>

其中 movl 和 call 只是放在那里，使之变得更适合人类阅读。好吧，我不知道你对此有何感想，但对我来说，这仍然很难理解。

当然有可能用这种迷之语言来编写程序——这就是过去人们在计算机上花费几百万美元，一台计算机体积大到要占用整个房间的那年代所做的——但我宁愿编写看起来像是这样的程序：

```swift
func handleMusicEvent(command: Int, noteNumber: Int, velocity: Int) {

  if command == NoteOn && velocity != 0 {
    playNote(noteNumber + transpose, velocityCurve[velocity] / 127)
    
  } else if command == NoteOff ||
           (command == NoteOn && velocity == 0) {
    stopNote(noteNumber + transpose, velocityCurve[velocity] / 127)
    
  } else if command == ControlChange {
    if noteNumber == 64 {
      damperPedal(velocity)
    }
  }
}
```

<center>上面的代码片段取自于一个声音合成器程序中</center>

它几乎看起来就像是某些有意义的东西。即使你以前从来没有编过程，你可以通过排序，弄清楚其中发生了什么。这几乎就是英语。（译者注：好好学习英语吧，也许我翻译本书是个错误）

Swift 是一门新兴的同时又非常热门的语言，它将传统的 object-oriented（面向对象）编程与函数式编程的各方面相结合。幸运的是，Swift 有许多与其他流行编程语言相同的东西，所以如果你已经熟悉 C#，Python，Ruby 或 Javascript，你会在使用 Swift 过程中体会到宾至如归的感觉。

Swift 并不是制作应用程序的唯一选择。直到最近，iPhone 和 iPad 应用程序都是使用 Object-C 编写的（译者注：乔老大留下宝贵财富，还是很有分量的），Object-C 是一门由 C 语言在 object-oriented 这一方面拓展而来的。由于是那个时代 C 语言的产物，Object-C 难免有着一些粗糙的棱角，并不真正符合现代开发商的需求。这就是为什么苹果创造了一种新的语言。

Object-C 仍然会存在一段时间，但显然，iOS 开发的未来是属于 Swift。所有 cool 孩子都已经在使用它了。

C++ 是另一种由 C 衍生出来的 object-oriented 编程语言。它非常强大，但作为一个刚入门的程序员，你可能会想要远离他。我只提一下它，因为 C++ 也可以用于编写 iOS 应用程序，并有着一段不羁之恋，C++ 与 Object-C 称之为 Object-C++，你可能会不时遇到。

我可以在 iOS Apprentice 的一开始深入讨论 Swift 的功能，但那样你可能会睡着。所以，我们来慢慢的解释语言，非常简单，等你适应了，再做更深入的讲解。

在一开始，一般概念——什么是 variable（变量），object（对象），如何调用 method（方法） 等——远比详细信息重要。虽然缓慢但毫无疑问，我会将 Swift 语言所有的秘密都揭露给你。

你准备好开始编写你生涯中的第一个 iOS 应用程序了吗？

## Bull's Eye 游戏

在第一课中，你将创建一个名为 Bull‘s Eye 的游戏。这是最终效果：

<div align="center"><img alt="完成的 Bull's Eye" src="http://imgur.com/YoEGCsp.png"/></div><center>完成的 Bull's Eye</center>

<br>

目标是滑动图中这个看起来像 bull's eye（牛眼）一样的 slider（滑块）（范围 1 ～ 100），使其尽可能的贴近系统给出的随机值。在上面的截图中，目标是将 bull's eye 滑动到 22 的地方，因为看不到 slider 的当前值，所以全靠目测了。

当你对你的估计有信心时，按下 “Hit Me!” button（按钮），弹出的窗口（也称为 alert（提醒））会告诉你，你获得了多少分：

<div align="center"><img alt="一个显示分数的 alert（弹出警报）" src="http://imgur.com/IGbMo3P.png"/></div><center>一个显示分数的 alert（弹出警报）</center>

<br>

越近目标值，你的得分就越高。在按下 OK（确定）按钮关闭警报弹出窗口后，新的轮次开始目标值被重新设置。游戏重复，直到玩家按下 “重新开始” 按钮（左下角的弯箭头），将分数重置为 0。

这个游戏可能不会让你在 App Store 上成为百万富翁，但却是你将来成为百万富翁的一个开端。

## 列出一个编程待办事项列表

**练习：**现在你已经看到了游戏的外观和了解了游戏的规则，列出你认为你需要做的一切，以备建立这个游戏。就算你画了一个空白，但仍给它一个镜头，也是 OK 的。（译者注：你有你自己的思考角度，你觉得怎么合理就怎么设计，即使它是空白的，但它对你而言就是有意义的）

接下来我将给你一个例子：

*应用程序需要在屏幕上放置 “Hit Me!” button，并在用户按下时显示警告弹出窗口。*

尝试想想还需要做些什么——如果你实际上并不知道该如何完成这些任务。首先一点，你需要确定下来你要做什么，而不是怎么做。

一旦你知道你想要什么，你也就可以一步一步弄清楚如何做到，尽管你不得不请教别人或者查阅有关资料。但是 “什么” 是你要首先确定的。（你会惊讶于不知道有多少人开始编写代码，却没有弄清实际上想要实现什么。难怪他们会陷入困境！）

每当我开始打造一个新的应用程序，我首先列出所有不同的那些我认为程序需要的功能。这将成为我的待办事项列表。有一个列表，将设计分为几个小的步骤是一个明智的方式以对处理复杂的项目。

你可能有一个很酷的想法，但当你坐下来写程序时，整个事情似乎要把你压垮。有这么多事要做… 从哪里开始？通过将工作量分为一个一个小的部分，你就可以使项目看起来没有那么令人生畏——你总是可以找到一个简单而小巧的步骤，以便创建一个良好的开端，并从那里开始。

这没什么大不了的，如果这个练习让你觉得困难。只是因为你是个刚开始学习这方面知识的新人而已！随着你对软件工作原理理解的加深，将能够更从容的将工作量合理分配并管理。

这是我的想法。我只是根据游戏的描述，并把它分割成一块一块：

- 在屏幕上放置一个 button，并将其标记为 “Hit Me!”。
- 当玩家按下 “Hit Me!” button 的时候，应用程序必须弹出一个警告窗口，通知玩家他的表现如何。以某种方式（暂时还不知道该如何做）计算出得分，并将得分放入警报窗口中。
- 在屏幕上放置文本，例如 “Score:” 和 “Round:” labels（标签）。这些文本会变化，例如分数，当玩家的得分时点数应该相应增加。
- 将 Slider 放在屏幕上，使其值在 1 到 100 之间。
- 在用户按下 “Hit Me!” button 后，读取 Slider 的值。
- 在每个回合开始时生成一个随机数，并将其显示在屏幕上，这是目标值。
- 将 Slider 的值与随机数进行比较，并计算出得分。让得分在警报窗口中显示。
- 将 “开始” 按钮放在屏幕上。点击它会重置得分，并从第一轮重新开始。
- 将应用程序以横屏显示。
- 美化。 :-)

我可能忽略了一两件事，但这看起来像是一个好的开端。即使对于这样简单的游戏，也有很多事需要你去做。使应用程序变得有趣，但同时也是一个大的工程！

## 只有一个 Button 的应用程序

让我们从刚才列出的列表的最顶端开始，做一个很简单的 v1.0 版本，只显示一个 button。当你按下它应用程序会弹出警报消息。这就是你现在要做的。一旦你完成了这个工作，你就可以在这个基础上继续构建游戏的其余部分。

应用程序将会看起来像这样：

<div align="center"><img alt="应用程序包含一个按钮（左），但按下时显示警报（右）" src="http://imgur.com/BlMYBTG.png"/></div><center>应用程序包含一个按钮（左），当按下时显示警报（右）</center>

<br>

是时候开始编码了！我假设你已经下载并安装了最新的 SDK 和开发工具。

在本教程中你将使用 Xcode 8.0 或更高版本。较新版本的 Xcode 也可以工作，但是任何比 8.0 版本更旧的都不适用。

因为 Swift 是一种非常新的语言，它往往在 Xcode 的版本之间变化。如果你的 Xcode 太旧了——或太新了！——那么本书中的所有代码并不一定都可以正常工作。（出于同样的原因，建议你不要使用 Xcode 的测试版，除了 Mac App Store 中的官方版本。）

➤ 启动 Xcode。如果在查找 Xcode 应用程序时遇到问题，可以在文件夹 **/Applications/Xcode** 或 Launchpad 中找到它。因为我一直使用 Xcode，我把它的图标放在我的 Dock 栏里以便访问。

Xcode 在启动时显示 “欢迎使用 Xcode”：

<div align="center"><img alt="Xcode 的欢迎问候" src="http://imgur.com/gHqKydO.png"/></div><center>Xcode 的欢迎问候</center>

<br>

➤ 选择 **Create a new Xcode project**（创建新的 Xcode 项目）。主 Xcode 窗口出现一个助手，让你选择一个模版：

<div align="center"><img alt="选择新项目的模版" src="http://i.imgur.com/hCShRSA.png"/></div><center>选择新项目的模版</center>

<br>

这有各种应用程序样式的模版。Xcode 将根据你选择的模版为你预先配置项目。新项目将包含你需要的许多源文件。这些模版很方便，节省了你大量的输入工作。它们是现成的起点。

➤ 选择 **Single View Application**（单一视图应用程序），然后按 **Next**（下一步）。

这会打开一个窗口，你可以在其中输入新应用的相关选项：

<div align="center"><img alt="配置新项目" src="http://i.imgur.com/viicYDF.png"/></div><center>配置新项目</center>

<br>

➤ 填写以下选项：

- Product Name（产品名称）：**BullsEye**。如果你想使用正确的英文，你可以命名项目为 Bull's Eye 而不是 BullsEye，但是最好避免在项目名称中出现空格和其他特殊字符。
- Team（团队）：如果你已经是 Apple 开发人员计划的成员，则会显示你的团队名称。现在，最好暂时留空；我们将在后面的教程回到这里。
- Organization Name（组织名称）：在此填写你自己的姓名或公司名称。
- Organization Identifier（组织标识）：我填的是 “com.razeware”。这是我用于我的应用程序标识。按照惯例，这是我的域名写在前面的方式。你应该在这里使用你自己的标识。选择你的唯一身份，你自己网站的域名（反过来）或只是自己的名字。你可以随时更改此设置。
- Languages（语言）：**Swift**
- Devices（设备）：**iPhone**

确保未选中底部的三个选项—— Use Core Data（使用 Core Data），Include Unit Tests（包括单元测试）和 Include UI Tests（包括 UI 测试）。你将不会在这个项目中使用这些。

➤ 按 **Next**（下一步）。现在 Xcode 会询问你在哪里保存你的项目：

<div align="center"><img alt="选择保存项目的位置" src="http://i.imgur.com/iDAlQoR.png"/></div><center>选择保存项目的位置</center>

<br>

➤ 为项目文件选择位置，例如 “Desktop”（桌面） 或 “Documents”（文档）文件夹。

Xcode 将使用你在上一步中输入的产品名称（在你的情况下为 BullsEye）自动为项目创建一个新文件夹，因此你不需要自己手动创建一个新文件夹。

在底部有一个复选框，说 “Create Git repository on My Mac”（在我的 Mac 上创建 Git 存储库）。你现在可以忽略此。你将在下一个教程中了解 Git 版本控制系统。

➤ 按 **Create**（创建）完成。

Xcode 现在将在你指定的文件夹中，创建一个名为 BullsEye 的基于单视图应用程序模板的新项目。

当完成时，屏幕如下所示：

<div align="center"><img alt="项目开始时的主 Xcode 窗口" src="http://i.imgur.com/TGqKHbX.png"/></div><center>项目开始时的主 Xcode 窗口</center>

<br>

如果您使用的 Xcode 版本高于8.0，则上述过程展示的图片与你在自己的计算机上看到的内容可能存在细微差异。放心，任何差异只会是表面的。

<code class="highlighter-rouge"><strong>注意：</strong>如果在左边的列表中没有看到名为 ViewController.swift 的文件，取而代之的是 ViewController.h 和 ViewController.m，那么当您制定项目（Objective-C）时选择了错误的语言。重新开始，并确保选择Swift作为编程语言。</code>

➤ 点击左上角的 **Run**（运行）按钮：

<div align="center"><img alt="按 Run（运行）以启动应用程序" src="http://i.imgur.com/XQbnEDB.png"/></div><center>按 <strong>Run</strong>（运行）以启动应用程序</center>

<br>

<code class="highlighter-rouge"><strong>注意：</strong>如果这是您第一次使用Xcode，它可能会要求您启用开发人员模式。单击 <strong>Enable</strong>（启用）并输入密码以允许Xcode进行这些更改。</code>

Xcode 将工作一会儿，然后它在 iOS 模拟器启动您全新的应用程序。就目前而言，可能该应用程序看起来还不像样——里面没有任何东西你可以使用的东西——但这是你的旅程中重要的第一个里程碑。

<div align="center"><img alt="基于 Single View Application 模板的应用程序是什么样子" src="http://i.imgur.com/5vUDxtf.png"/></div><center>基于 Single View Application 模板的应用程序是什么样子</center>

<br>

当你按下运行按钮后如果 Xcode 说 “Build Failed”（建立失败）或 “Xcode cannot run using the selected device”（Xcode 不能使用选定的设备运行） ，然后确保选择器在窗口的顶部为 BullsEye > iPhone SE（或任何其他型号），而不是 Generic iOS Device（通用 iOS 设备）：

<div align="center"><img alt="让 Xcode 在模拟器上运行应用程序" src="http://imgur.com/k2BJR8p.png"/></div><center>让 Xcode 在模拟器上运行应用程序</center>

<br>

如果你的 iPhone 当前通过 USB 电缆连接到你的 Mac，Xcode 可能会试图在你的 iPhone 上运行应用程序，这可能无法工作，因为缺少了一些额外的设置。在本教程的最后，我将告诉你如何让应用程序在你的 iPhone 上运行，所以你可以把它展示给你的朋友，但现在只需坚持使用模拟器。

➤ **Run** 按钮旁边是 **Stop**（停止）按钮（方形）。 按此退出应用程序。

在你的手机上，你可以使用主屏幕按钮退出应用程序（在模拟器上从菜单栏选择 **Hardware**（硬件）→ **Home**（主页）），但这不会实际终止应用程序。它会从模拟器的屏幕上消失，但应用程序保持暂停在模拟器的内存，就像在一个真正的iPhone。

直到你按 Stop，Xcode 的顶部活动查看器说 “Running BullsEye on iPhone SE”（在iPhone SE上运行BullsEye）：

<div align="center"><img alt="Xcode 活动查看器" src="http://imgur.com/Mxn6Ddf.png"/></div><center>Xcode 活动查看器</center>

<br>

它不是真的必要停止的应用程序，就像你可以回到 Xcode 和更改源代码，而应用程序仍在运行。 但是，在你再次按Run之后，这些更改才会生效。这将终止任何运行的应用程序版本，构建新版本，并在模拟器启动它。

<code class="highlighter-rouge"><strong>当你按 Run 时会发生什么？</strong></code>

`Xcode 将首先编译你的源代码——即：将它——从 Swift 转换为 iPhone（或模拟器）可以理解的机器代码。即使用于编写 iPhone 应用程序的编程语言是 Swift 或 Objective-C，iPhone 本身也不会使用这些语言。翻译步骤是必要的。`

`编译器是 Xcode 的一部分，将 Swift 源代码转换为可执行的二进制代码。它还收集组成应用程序的所有不同组件——源文件，图像，故事板文件等，并将其放入所谓的 “application bundle”（应用程序包）。`

`这整个过程也被称为构建应用程序。如果有任何错误（例如拼写错误），构建将失败。如果一切都按计划进行，Xcode 将应用程序包复制到模拟器或 iPhone 并启动应用程序。所有这一切只需单击一下 Run 按钮。`

## 添加 Button

我相信你几乎没有印象，因为我有一个只是显示无聊白色屏幕应用程序，所以让我们添加一个 button。

Xcode 窗口的左侧被命名为 **Navigator Area**（导航区域）。顶部的图标行决定了哪个导航器是可见的。当前是 **Project Navigator**（项目导航器），它显示项目中的文件列表。

这些文件的组织大致对应于硬盘上的项目文件夹，但不一定总是这样。你可以移动文件，并尽情地将它们放入新的组。后续我们将更多地讨论你项目中的不同文件。

➤ 在 **Project Navigator** 中，找到名为 **Main.storyboard** 的项目，然后单击以选择它：

<div align="center"><img alt="Project navigator 列出项目中的文件" src="http://imgur.com/zQbYOva.png"/></div><center><strong>Project navigator</strong> 列出项目中的文件</center>

<br>

像一个超级英雄在电话亭里改变他的衣服，主编辑窗格现在转换为界面生成器。这个工具允许你将用户界面组件（例如 button）拖放到 **Interface Builder** 中。（OK，虽然这个比方打的不怎样，但是我只是想说 Interface Builder 是一个超级工具。）

➤ 如果它还不是蓝色，请单击 Xcode 工具栏中的 **Hide or show utilities** （隐藏或显示）实用程序按钮：

<div align="center"><img alt="单击此按钮显示 Utilities pane（实用程序窗格）" src="http://imgur.com/NELiQRU.png"/></div><center>单击此按钮显示 <strong>Utilities pane</strong>（实用程序窗格）</center>

<br>

按下这些在工具栏上的按钮将会改变 Xcode 的外观。特别是这一个，它会在 Xcode 窗口的右侧打开一个新窗格。

你的 Xcode 现在看起来应该像是这样：

<div align="center"><img alt="在 Interface Builder 中编辑 Main.storyboard" src="http://imgur.com/kTdCj6O.png"/></div><center>在 Interface Builder 中编辑 Main.storyboard</center>

<br>

这是你的应用程序的 storyboard（故事板）。storyboard 包含应用程序所有的屏幕设计，并显示应用程序是如何从一个屏幕到另一个屏幕，通过一个大箭头。

目前，storyboard 只包含一个屏幕或 scene（场景），由 Interface Builder Canvas（画布）中间的一个矩形表示。

<code class="highlighter-rouge"><strong>注意：</strong>如果你没有看到标记为 “View Controller”（视图控制器） 的矩形，眼前只有一个空白的 Canvas，则使用鼠标或触控板滚动 storyboard。相信我，它一定在某处！还要确保你的 Xcode 窗口足够大。因为 Interface Builder 占用了很多空间...</code>

该 scene 目前有一部 iPhone 6s 或 iPhone 7 的大小。为了保持清爽简洁，你会首先为 iPhone SE 设计一个稍小的屏幕的应用程序。稍后你将会让这款应用程序也是配更大的 iPhone 6s，7 和 Plus。

➤ 在 Interface Builder 窗口底部，单击 **View as**（查看为）**：iPhone 6s** 以打开打开以下面板：

<div align="center"><img alt="选择设备类型" src="http://imgur.com/tVGJKrP.png"/></div><center>选择设备类型</center>

<br>

选择 **iPhone SE**，第二小的 iPhone 。scene 的矩形现在变得有点小了。这对应于 iPhone 5，iPhone 5s 和 iPhone SE 机型的屏幕尺寸。

➤ 在 Xcode 工具栏中，确保它说 **BullsEye > iPhone SE**（在 Stop 按钮旁边）。如果默认选项不是，那么单击它，并从列表中选择 iPhone SE：

<div align="center"><img alt="将模拟器切换到iPhone SE" src="http://imgur.com/agi8Tbk.png"/></div><center>将模拟器切换到 iPhone SE</center>

<br>

现在当你运行应用程序，它将运行在 iPhone SE 模拟器（试试吧！）。

我们接着谈 storyboard：

➤ 在 Utilities pane 底部，将找到 **Object Library**（对象库）（确保选中了第三个看起来像圆形的按钮）：

<div align="center"><img alt="Object Library" src="http://imgur.com/3liGfUb.png"/></div><center>Object Library</center>

<br>

滚动 Object Library 列表中的项目，直到看到 button。

➤ 将 button 拖动到位于工作区域的 scene 的矩形的顶部。

<div align="center"><img alt="拖动 button 到 scene 顶部" src="http://imgur.com/lbNySmJ.png"/></div><center>拖动 button 到 scene 顶部</center>

<br>

看，添加一个 button 多么简单，只需要拖放。 这也适用于所有其他用户界面元素。你会做很多这样的事情，所以花一些时间来熟悉这个过程。

➤ 拖放一些其他 controls（控件），如 labels，sliders 和 switches，只管拖动他们就对了。

这应该会给你一些有关 UI controls 的想法，因为 iOS 支持使用它们。请注意，Interface Builder 会帮助您布局 controls，通过将 controls 对齐到 view 的边缘和其他 objects。这是一个非常方便的工具！

➤ 双击刚刚放置的 button 以编辑其标题为 “Hit Me!”。

<div align="center"><img alt="带有新标题的 button" src="http://imgur.com/ycaJMiF.png"/></div><center>带有新标题的 button</center>

<br>

你的按钮可能有一个边框：

<div align="center"><img alt="带有边界矩形的 button" src="http://imgur.com/1pBSWja.png"/></div><center>带有边界矩形的 button</center>

<br>

这个边框不是 button 的一部分，它只是在那里显示 button 有多大。你可以使用 **Editor** **→ Canvas → Show Bounds Rectangles**（显示矩形边框）菜单选项打开或关闭这些矩形。

当你完成与 Interface Builder 的互动后，按下 Xcode 工具栏上的 Run 按钮。应用程序现在应该出现在模拟器中，完成你的 “Hit Me!” button。但是，当你点击 button 它不做任何事情。为此，你必须写一些 Swift 代码！

## 源代码 Editor

一个 button，没有做任何事情，任何人按它都没有用，所以让我们让它显示一个 alert 弹出。 在完成的游戏中，alert 将显示玩家的分数，但现在我们将限制自己一个简单的文本消息（传统的“Hello, World!”）。（译者注：有这么一个故事：有一天，某程序员爱慕已久的女神主动和他打了招呼。女神：“Hello.”，程序员：“World!”，那么这个故事就到此打住了）

➤ 在 **Project navigator**，单击 **ViewController.swift**。

Interface Builder 将消失，Editor 区域现在展现出一堆明亮的彩色文本。这是你的应用程序的 Swift 源代码：

<div align="center"><img alt="源代码 Editor" src="http://imgur.com/0XoNazy.png"/></div><center>源代码 Editor</center>

<br>

➤ 将以下行直接添加到文件中最后一个括号之上：

```swift
@IBAction func showAlert() {
}
```

**ViewController.swift** 的源代码现在应该如下所示：

```swift
//
//  ViewController.swift
//  BullsEye
//
//  Created by <you> on <date>.
//  Copyright © <year> <you>. All rights reserved.
//
import UIKit

class ViewController: UIViewController {

  override func viewDidLoad() {
    super.viewDidLoad()
    // Do any additional setup after loading the view, typically
	from a nib. 
  }

  override func didReceiveMemoryWarning() {
    super.didReceiveMemoryWarning()
    // Dispose of any resources that can be recreated.
  }

  @IBAction func showAlert() {
  }
}
```

初尝 Swift 的感觉如何？合你口味吗？ 在我可以告诉你这是什么意思之前，我首先要介绍一个有关 view controller 的概念。

<code class="highlighter-rouge"><strong>Xcode 会自动保存</strong></code>

<code class="highlighter-rouge">你不必保存文件，在你对它们进行更改后，因为当你按下 Run 按钮后 Xcode 将自动保存任何修改的文件。然而，Xcode 不是最稳定的软件，有时候它可能会在保存你的更改之前崩溃，所以我仍然想按 <strong>⌘ + S</strong> 定期保存我的文件。</code>

## View controllers

你已经编辑 **Main.storyboard** 文件来构建应用程序的用户界面。它只是一个白色 background 上的 button，但它确实是一个实实在在的用户界面。你还向 **ViewController.swift** 添加了源代码。

这两个文件——storyboard 和 Swift 文件——一起形成了 *view controller* 的设计和实现。 构建 iOS 应用程序的很多工作是创建 view controller。 view controller 的工作是在应用程序中管理单个屏幕。

以一个简单的食谱应用程序为例。当你启动它时，其主屏幕列出可用的食谱。点击一个食谱打开一个新的屏幕，显示食谱详细的一个美味的照片和烹饪说明。每个屏幕由其自己的 view controller 来管理。

<div align="center"><img alt="view controller 在一个简单的食谱应用程序中的应用" src="http://imgur.com/dOpNhlP.png"/></div><center>view controller 在一个简单的食谱应用程序中的应用</center>

<br>

相比之下，这两个屏幕是非常不同的。一个是几个项目的列表；另一个呈现单个项目的详细视图。

这就是为什么你还需要两个 view controller：一个知道如何处理列表，另一个可以处理图像和烹饪说明。 iOS 的设计原则之一就是，应用程序中的每个屏幕都有自己的 view controller。

目前 Bull's Eye 只有一个屏幕（顶部有一个白色 button 的那个），因此只需要一个 view controller。该 view controller 简称为 “ViewController”（译者注：这里看起来比较怪，实际上后者只是一个命名，你可以随意修改。前者则为专有名词），storyboard 和 Swift 文件一起工作来实现它。

简单地说，Main.storyboard 文件包含 view controller 的用户界面的设计，而ViewController.swift 包含其功能——让用户界面按照设定来工作的逻辑，它是使用 Swift 语言来编写的。

因为你使用 Single View Application 模板，Xcode 自动为你创建 view controller。 稍后，你将为游戏添加第二个屏幕，你将为此创建自己的 view controller。

## 建立关联

你刚刚所添加到 ViewController.swift 的源代码的作用是让 Interface Builder 知道 controller 有一个名字为 “showAlert” 的 action（操作），它可能会显示一个 alter 弹出窗口。你现在将要做的就是将 button 连接到该 action。

➤ 单击 **Main.storyboard** 返回到 Interface Builder。

左边应该有一个 pane，即 **Outline pane**（大纲窗格），其中列出了所有项目你的 stpryboard。如果没有看到该 pane，请单击 Interface Builder canvas 左下角的小切换按钮以显示它。

<div align="center"><img alt="用来显示 Outline pane 的按钮" src="http://imgur.com/uThAxbE.png"/></div><center>用来显示 Outline pane 的按钮</center>

<br>

➤ 单击 **Hit Me** button 将其选中。

选中 “Hit Me” button 后，按住 Ctrl 键，单击 button 并向上拖动到 Outline pane 中的 View Controller 项。你应该会看到 button 和 View Controller 之间出现一条蓝线。

（如果你不想按住 Ctrl，你也可以右键单击和拖动，但在开始拖动之前，请不要放开鼠标按键。）

<div align="center"><img alt="从 button 开始按住 ctrl 并拖动到 View Controller" src="http://imgur.com/GXEDkR6.png"/></div><center>从 button 开始按住 ctrl 并拖动到 View Controller</center>

<br>

一旦你在 View Controller 上，放开鼠标按键，会出现一个小菜单。 它包含两个部分，  “Action Segue” 和 “Sent Events”（发送事件），每个下面有一个或多个选项。 你对 Sent Events 下的 **showAlert** 选项感兴趣。这是你先前在 ViewController.swift 的源代码中添加的 action 的名称。

<div align="center"><img alt="带有 showAlert action的弹出菜单" src="http://imgur.com/tbiY4J1.png"/></div><center>带有 showAlert action 的弹出菜单</center>

<br>

➤单击 showAlert 以选择它。这表明 Interface Builder 在 button 和 @IBAction func show Alert() 之间进行关联。

从现在开始，每当 button 被点击时，将执行 showAlert action。这就是如何使 button 和其他controls 互动：你在 view controller 的 Swift 文件中定义一个动作，然后在Interface Builder中进行连接。

你可以看到连接关系，通过 Xcode 窗口右侧的实用程序窗格中的 **Connections inspector**（连接检查器）。

➤ 单击 pane 顶部的小箭头形按钮以切换到 Connections inspector：

<div align="center"><img alt="inspector 显示从 button 到任何其他 object 的连接" src="http://imgur.com/8qKlFD2.png"/></div><center>inspector 显示从 button 到任何其他 objects 的连接</center>

<br>

在 Sent Events 部分中，“Touch Up Inside”（触摸内部）事件现在已连接到 showAlert action。你同样可以在 Swift 文件中查看连接。

➤ 选择 ViewController.swift 以编辑它。

注意在行 @IBAction func showAlert() 的左边，有一个实心圆？ 点击该圆以显示此 action 所连接的内容。

<div align="center"><img alt="实心圆表示动作连接到某物" src="http://imgur.com/079R0Yo.png"/></div><center>实心圆表示动作连接到某物</center>

<br>

## Button 上的行为

你现在有一个带有 button 的屏幕。该 button 被关联到名为 showAlert 的 action 上，当用户点击该 button 时将执行该 action。

然而，目前而言，action 是空的，什么也不会发生（不信试试）。你需要向应用程序提供更多说明。

➤ 在 ViewController.swift 中，将以下行添加到 showAlert 中：

```swift
@IBAction func showAlert() {
  let alert = UIAlertController(title: "Hello, World",
                                message: "This is my first app!",
                                preferredStyle: .alert)
                                
  let action = UIAlertAction(title: "Awesome", style: .default,
                             handler: nil)
                             
  alert.addAction(action)
  
  present(alert, animated: true, completion: nil)
}
```

<center>新加入的这几行提供了此 action 的实际功能。</center>

{} 括号之间的命令告诉 iPhone 做什么，它们从上到下依次执行。

showAlert 中的代码创建一个标题为 “Hello，World” 的 alert，它包含一条 “This is my first app!” 消息和一个 label 为 “Awesome” 的 button。

如果你不确定标题和消息之间的区别：都显示文本，但标题稍大，而且采用粗体。

➤ 单击 Xcode 工具栏上的 Run 按钮。如果你没有任何的拼写错误，你的应用程序应该会在模拟器中启动，当你点击 button，应该会看到 alert。

<div align="center"><img alt="alert 弹出动作" src="http://i.imgur.com/suZqPl0.png"/></div><center>alert 弹出动作</center>

<br>

恭喜，你刚刚编写了属于你的第一个 iOS 应用程序！你刚刚做的事可能在你看来是莫名其妙的，但这不重要。 我们一次只走一小步。

你可以从一开始列出的待办事项列表中删除前两个项目：在屏幕上放置一个 button，并在用户点 button 钮时显示 alert。

休息一下，让它沉淀下来，当你准备好学习更多的时候回来！你只不过是刚刚迈出一小步而已...

<code class="highlighter-rouge"><strong>注意：</strong>为了防止你卡住，我已经在本教程附带的源代码文件夹中为本教程中的几个检查点提供了完整的 Xcode 项目。这样，你可以拿你的应用程序的版本和我的做对比，或者——如果你真的弄乱了一些东西——可以从一个你拿的准的版本入手。</code>

<code class="highlighter-rouge">你可以在 <strong>01 - One Button App</strong> 文件夹中找到你迄今为止所做的应用程序的项目文件。</code>

## 问题？

如果 Xcode 在按下 Run 后出现 “Build Failed” 错误消息，请确保输入的所有内容是正确的。即使是最小的错误也会把 Xcode 弄晕。它可以是相当压倒性的有意义的错误消息。源代码顶部的一个小错字可能会引起在该文件的其他位置产生多个错误。

典型的错误是大小写不同。Swift 编程语言是区分大小写的，这意味着它看到 Alert 和 alert 作为两个不同的名称。Xcode 使用 “\<something> undeclared” 或 “Use of unresolved identifier”（使用未解析的标识符）来报出这个错误。

当 Xcode 说 “Parse Issue” 或 “Expected \<something>” 的时候，你可能忘了一个花括号 } 或括号 ）。不匹配开括号和闭括号是一个常见的错误。

（Tips：如果将文本光标移动到结束括号上，Xcode 将以高亮标记相应的开始括号）

这样的小细节在你编程时非常重要。即使一个错位字符它也可以阻止 Swift 编译器构建你的应用程序。

幸运的是，这种错误很容易找到。

<div align="center"><img alt="Xcode 会确保你不会忽略掉错误" src="http://imgur.com/KWjPWMm.png"/></div><center>Xcode 会确保你不会忽略掉错误</center>

<br>

当 Xcode 检测到错误时，将左侧窗格切换到 **Issue navigator**（问题导航器），你的项目文件就是这样。此列表显示 Xcode 找到的所有错误和警告。（你可以回到项目文件，通过顶部的小按钮。）

显然，我忘了某处的逗号。

点击错误消息，Xcode 会带你到源代码中出现错误的行。它甚至建议你需要做什么来解决它：

<div align="center"><img alt="Fix-it 对于这个问题建议的一条解决方案" src="http://imgur.com/tIWHKT2.png"/></div><center>Fix-it 对于这个问题建议的一条解决方案</center>

<br>

有时，当你构建失败，你很难找到你做错了什么，但幸运的是，Xcode 提供这样的助手。

<code class="highlighter-rouge"><strong>Errors（错误）和 warnings（警告）</strong></code>

`Xcode区分 errors（红色）和 warnings（黄色）。errors 是致命的。 如果你有一个，你不能运行应用程序。warnings 是信息。Xcode只是说，“你可能不是想这样做，但仍然继续。`

`在我看来，最好把所有 warnings 看作是 errors。在继续操作之前修复 warnings，并且只有在出现零个 errors 和零个 warnings 时才运行应用程序。这不保证应用程序不会有任何错误，但至少它不会是愚蠢的。`

## 应用程序如何工作？

在这一点上，将会有一些体会关于应用程序的背后到底发生了什么。

应用程序本质上由可以向彼此发送消息的 **objects** 组成。你的应用程序中的许多 objects 由iOS提供，例如 button（UIButton 对象）和 alert 弹出窗口（UIAlertController 对象）。对于一些 objects，你必须自己编程，如 view controller。

这些 objects 通过将消息传递给彼此进行通信。当用户点击应用程序中的 “Hit Me” button 时，例如，该 UIButton object 发送消息到你的 view controller。view controller 可以通知更多的 objects。

在 iOS 上，应用程序是事件驱动，这意味着这些 objrcts 侦听某些事件并进行处理。

听起来很奇怪，一个应用程序花大部分时间做… 什么没有。它只是坐在那里等待某事件发生。当用户点击屏幕时，应用程序弹出几毫秒的动作，然后它再次回到睡眠，直到迎来下一个事件。

在此方案中你所做的部分就是，由你编写的源代码将在对象接收到此类事件的消息时执行。

在应用程序中，button 的 Touch Up Inside 事件连接到 view controller 的 showAlert action。 所以当 button 识别它已被轻敲时，它发送 showAlert 消息到你的 view controller。

在 showAlert 内部，view controller 发送另一个消息，addAction 到 UIAlertController 的 object。为了显示警报，view controller 发送当前消息。

你的整个应用程序将由以这种方式来通信的对象所组成。

<div align="center"><img alt="应用中事件的一般流程" src="http://imgur.com/peQXMv5.png"/></div><center>应用中事件的一般流程</center>

<br>

也许你已经在你的网站上使用过 PHP 或 Ruby 脚本。这个基于事件的模型与 PHP 脚本的工作原理不同。PHP 脚本将从上到下运行，一个接一个地执行语句，直到它到达终点，然后退出。

应用程序，另一方面，不退出，直到用户终止它们（或它们崩溃！）。它们花费大部分时间等待输入事件，然后处理这些事件并回到睡眠状态。

来自用户的输入，大多数是触摸和敲击的形式，是你的应用程序中的最重要的事件源，但也有其他类型的事件。例如，当用户接收到来电时，当它必须重新绘制屏幕时，当定时器倒计时… 操作系统就会通知你的应用程序。

你的应用程序执行的所有 action 都是由某个事件触发而来的的。

## 按照待办事项列表工作

现在你已经完成了第一个任务，在屏幕上放置一个 button，并使其显示一个 alert，你只需下去列表，勾选其他项目。

你不必真的要以某种特定的顺序去做，虽然一些事情在别的事情之前做有意义。 例如，如果你还没有 slider，则无法读取 slider 的位置。

所以，让我们添加其余的 controls——slider 和 text labels，并将这个应用程序变成一个真正的游戏！

当你完成后，应用程序将如下所示：

<div align="center"><img alt="配有标准 UIKit（界面工具包）controls 的游戏屏幕" src="http://imgur.com/WfRn9F7.png"/></div><center>配有标准 UIKit（界面工具包）controls 的游戏屏幕</center>

<br>

嘿，等一下...... 这看起来并不像我答应你的那样，展示给你看的游戏那般漂亮！区别在于这都是些标准的 UIKit controls。他们看起来像是直接开箱的样子。

你可能已经看过这个面板，因为它非常适合常规的应用程序。但是因为默认的死沉沉的样子对于一个游戏来说有点枯燥无聊，所以你会在后续课程给它加一些调味料。

<code class="highlighter-rouge"><strong>UIKit 和其他 frameworks（框架）</strong></code>

`iOS 提供了许多 frameworks 或 “kits” 形式的构建块。UIKit frameworks 提供了用户界面的 controls，如 buttons，labels 和 navigation bar。它管理 view controller，通常负责处理应用程序的用户界面。（ UI 代表：用户界面。）`

`如果你不得不得从头开始写所有的东西，你或许要忙上一会儿。相反，你可以在系统提供的 frameworks 之上构建你的应用程序，并利用苹果工程师已经为你做完了的现成的东西。`

`任何你看到的以 UI 开头的 objects，例如 UIButton，都来自 UIKit。当你编写 iOS 应用程序时，UIKit framework 将是耗费你大部分时间的地方，但也有些人不会。`

`其他 frameworks 的示例是 Foundation，它提供了构建应用程序的许多基本构建块; 用于在屏幕上绘制基本形状（如线条，渐变和图像）的核心图形; 播放声音和视频的 AVFoundation; 和许多其它的。`

`iOS 的完整 frameworks 集合统称为 Cocoa Touch。`

---

**译者注：**

<center><strong>iPhone 技术层</strong></center>

| Cocoa Touch |
| :---------: |
|    **⇩**    |
|   **多媒体**   |
|    **⇩**    |
|  **核心服务**   |
|    **⇩**    |
|  **核心 OS**  |

<br>

<center><strong>Cocoa 包含 Foundation 和 ApppKit framework，可用于开发 macOS 系统的应用程序。</strong></center>

<br>

<center><strong>Cocoa Touch 包含 Foundation 和 UIKit framework，可用于开发 iOS 的开发环境。</strong></center>

---

<br>

## 竖屏（portrait）vs. 横屏（landscape）

请注意，应用程序的尺寸已更改：iPhone 是倾斜的侧面，屏幕更宽，但不高。 这称为 *landscape* 方向。

你毫无疑问在 iPhone 上看到了 landscape 应用程序。 对于游戏而言这是一个常见的显示方向，但通常来说，许多其他类型的应用程序，除了工作在常规的 “直立” *portrait* 方向之外也工作在 landscape 模式下。

例如，许多人喜欢用他们的设备翻转写电子邮件，因为更宽的屏幕允许更大的键盘就使得打字更容易。（译者注：然而国人更青睐九宫格）

在 portrait 方向，iPhone SE 屏幕包括水平 320 点和垂直 568 点。对于 landscape，这些尺寸对调。

<div align="center"><img alt="portrait 和 landscape 下的屏幕尺寸" src="http://imgur.com/oaPAtRW.png"/></div><center>portrait 和 landscape 下的屏幕尺寸</center>

<br>

那么什么是点呢？

对于较旧的设备——最高到 iPhone 3GS 和相应的 iPod touch 型号，以及第一代 iPad 而言一点对应一个像素。因此，这些低分辨率设备看起来不是很清晰，因为它们的大又粗糙的像素。

我相信你知道一个像素是什么。如果你不知道的话：它是屏幕组成的最小的元素。你的 iPhone 显示的是一个大矩阵的像素，每个像素都可以有自己的 color（颜色），就像一个电视屏幕。 改变这些像素的 color 值在显示器上产生可见图像。像素越多，图像看起来越好越细腻。

在 iPhone 4 和更高版本的高分辨率 Retina 显示器上，一个点实际上对应于水平和垂直的两个像素，因此总共有四个像素。它在非常小的空间中包装了大量像素，使得显示更加清晰，这就是 Retina 设备普及的原因。

在 Plus 上它甚至更疯狂：它有一个 3x 分辨率，每个点有九个像素。我的天！你需要老鹰的眼睛，才能分辨这个花哨的 Retina 高清显示器上的个别像素。几乎不可能弄清楚一个像素在哪里结束，下一个像素开始，这是多么的微小。

它不仅是不同的 iPhone 模型之间不同的像素数量。多年来，他们已经拥有了不同的外形，从一开始的小的 3.5 英寸屏幕，到 iPhone 6s Plus 和 7 Plus 的5.5英寸。

不同尺寸对应的宽和高的点数：

<div align="center"><img alt="" src="http://imgur.com/WCRTKv6.png"/>

</div>

<br>

在 iOS 的早期时代，只有一个屏幕尺寸。 但是，“一刀切” 的时代已经过去了。现在我们有各种各样的屏幕尺寸要处理。

请记住，UIKit 使用点而不是像素，因此你只需要担心以点为单位测量的屏幕尺寸之间的差异。实际的像素数量只对平面设计师很重要，因为图像仍然是以像素为单位测量的。

开发人员在工作在点层次上，设计师工作在像素层次上。

点和像素之间的差异可能有点混乱，但到现在为止如果这是唯一使你困惑的事情，那么我做的教程还不错。 ;-)

在本教程中，你最初将只使用大小为 320×568 点的 iPhone SE 屏幕——只是为了简单。稍后在教程中，你还将使游戏适配其他尺寸的iPhone。

## 将应用转换为 landscape

要将应用程序从 portrait 转为 landscape，你必须做两件事：

1. 在 **Main.storyboard** 将 view 设置为 landscape 而不是 portrait。
2. 更改应用程序的 **Supported Device Orientations**（支持的设备方向）设置。

➤ 在 Interface Builder 中打开 **Main.storyboard**。在 **View as: iPhone SE** 面板中，将 **Orientation** 更改为 lanscape：

<div align="center"><img alt="在 Interface Builder 中更改 orientation" src="http://imgur.com/ronMSFi.png"/></div><center>在 Interface Builder 中更改 orientation</center>

<br>

这将更改 view controller 的尺寸。它会把按钮放在一个尴尬的地方。

➤ 将按钮移回 view 的中心，因为有着不整洁的用户界面的程序在当下难以有一席之地。

<div align="center"><img alt="在 landscape 下的 view" src="http://imgur.com/70hdZxh.png"/></div><center>在 landscape 下的 view</center>

<br>

关心了一下 view 的布局。

➤ 在 iPhone SE 模拟器上运行应用程序。屏幕不显示为 landscape，按钮也不再位于中心。

但是，如果你将模拟器旋转为 landscape，那么一切都会看起来像预想的一样了。

➤ 从屏幕顶部的模拟器菜单栏中选择 **Hardware **→ Rotate Left（向左旋转）或 Rotate Right（向右旋转），或按住 ⌘，然后按键盘上的向左或向右箭头键。这将旋转模拟器。

请注意，在 landscape 方向，应用程序不再显示 iPhone 的状态栏。这给应用程序的用户界面留出更多的空间。

你还应该做一件事。有一个配置选项，告诉 iOS 你的应用程序支持的方向。你通过模板所创建的新应用始终都支持纵向和横向。

➤ 单击 **Project navigator** 顶部的蓝色的 **BullsEye** 项目图标。Xcode 窗口的 editor pane 现在显示了项目的一些设置。

➤ 确保选择的是 **General**（常规）选项卡：

<div align="center"><img alt="项目的设置" src="http://imgur.com/UJlJeHf.png"/></div><center>项目的设置</center>

<br>

在 **Deployment Info**（部署信息）部分中，有一个用于 **Device Orientation** 的选项。

➤ 仅检查 Landscape Left 和 Landscape Right 选项，并保留未选中的 Portrait 和 Upside Down（倒置）选项。

再次运行应用程序，它将非常正确的从一开始就以 landscape 方向启动。

## Objects，data 和 method


是时候来一些编程理论了。是的，你逃不过的。

Swift 是一种所谓的 “object-oriented” 编程语言，这意味着你做的大多数事情的时候都涉及到某种东西。我已经反复提了几次，一个应用程序包含着能彼此发送消息的 objects。

编写 iOS 应用程序时，将使用系统为你提供的 objects，例如 UIKit 中的 UIButton object，并且你将创建自己的对象，例如 view controller。

那么 object 究竟 *是* 什么呢？想像一个 object 作为你的程序的构建块。（译者注：金字塔上的石块，积木建筑中的积木块）

程序员喜欢将相关的功能分组为 object。这个 object 负责解析文件，那个 object 知道如何在屏幕上绘制图像，而另一个 object 可能会执行困难的计算。

每个 object 负责程序的特定部分。在一个完整的应用程序，你会有许多不同类型的 objects（几十或甚至数百）。

即使你的小启动器应用程序也已经包含几个不同的 objects。你花了最多的时间，到目前为止的是 ViewController。Hit Me button 也是一个 object，alert 弹出。 和你的 alert text——“Hello, World!” 和 “This is my first app!”——他们都是 object。

该项目还有一个名为 AppDelegate 的 object，不过你将在此课程中忽略它（但如果你好奇，可以随意查看它的源文件）。这些 objects 无处不在！

一个 object 可以具有 data 和 functionality（功能）：

- 举个说明 data 的例子，就是你之前添加到 view controller 的 Hit Me button。当你将 button 拖到 storyboard 中时，实际上那一刻它成为了 view controller 的 data 中的一部分。data 包含内容。在这种情况下，view controller 包含 button。
- 关于 functionality 的一个例子就是，你添加用来响应 button 上的轻击的 showAlert action。 functionality 用来 *做* 某事。

button 本身也有 data 和 functionality。button data 的例子就是，它的标签的文本和 color，它在屏幕上的位置，宽度和高度等。该 button 还具有 functionality：它可以识别用户点击它，并将触发一个动作作为响应。

为 object 提供 functionality 的东西通常称为 *method*。 其他编程语言可以将其称为 “procedure”（过程）或 “subroutine”（子程序）或 “function”（函数）。你还将看到 Swift 中使用的术语function; 一个 method 只是一个属于一个 object 的 function，一对多的关系。

你的 showAlert action 就是一个活生生的关于 method 的例子。你可以说它是一个 function，因为那一行这么写道 func（“function” 的缩写），名称后面跟着的是括号：

<div align="center"><img alt="所有 method 定义都以 func 开头，并带有括号" src="http://imgur.com/N8DsltG.png"/></div><center>所有 method 定义都以 func 开头，并带有括号</center>

<br>

如果你再看看 **ViewController.swift** 的其余部分，你会看到其他几个方法，如 viewDidLoad() 和 didReceiveMemoryWarning()。

这些目前没啥作用；Xcode 模板只是将放在那里为你提供方便。这些特定的 method 经常被 view controller 使用，所以很可能你需要在某个时候来为它们添加内容。

Method 的概念可能仍然有点怪异，所以这里有一个例子：

<div align="center"><img alt="每一方都需要冰淇淋！" src="http://imgur.com/qPTRt9B.png"/></div><center>每一方都需要冰淇淋！</center>

<br>

你（或至少一个名字为 “你” 的 object）想开一个聚会（译者注：这里给出原文，所以不要问我为什么这个方法名这么奇怪，叫做throwParty：You (or at least an object named “You”) want to throw a party），但你忘了买冰淇淋。幸运的是，你邀请了名为史蒂夫的 object，他恰好住在一家便利店旁边。这不会是一场没有冰淇淋的聚会，所以在你的聚会准备期间的某个时候，你给 object Steve 一个消息，要求他带一些冰淇淋。

计算机现在将 object 切换到 Steve，并从上到下逐个执行他的 buyIceCream() method 的命令。

当他的 method 完成后，计算机返回你的 throwParty() method，并继续，所以你和你的朋友可以吃史蒂夫带回来的冰淇淋。

名为 Steve 的 object 也有 data。在他去商店之前，他有钱。在商店，他交换这些钱 data 为其他，更重要的 data：冰淇淋！做完这个交易后，他把冰淇淋的 data 带到了派对上（如果他一直吃着它，你的程序有一个bug）。

“发送消息” 听起来比它原本的意思更难懂。但这是一个很好的方式来思考 objects 如何沟通，但其中真的没有任何鸽子或邮递员参与。计算机只是从 throwParty() method 跳转到buyIceCream() method，然后再返回。

通常使用术语 “calling a method”（调用方法）或 “invoking a method”（调用方法）。这意味着与发送消息完全相同的事情：计算机跳转到你调用的 method，并返回到该方法结束时它停止的地方。

重要的是要记住的是，对象有 method（涉及购买冰淇淋的步骤）和 data（实际的冰淇淋和用来买它的钱）。

Objects 可以互相看看对方的 data（在某种程度上，就像如果你偷看 Steve 的钱包， 它可能不赞成），并可以要求其他 objects 执行他们的 methods。这就是你让你的应用程序做事情。

## 添加其余的 controls

你的应用程序已经有了按钮，但你仍需要新增其他 UI controls（也称为 “views”）。再次回到这个屏幕，这次不同的 controls 我在 views 上都给出了相应的 comments（注释）：（译者注：暂时把 views 理解为视图中的 UI 控件吧）

<div align="center"><img alt="游戏屏幕中的不同视图" src="http://imgur.com/C2mOduT.png"/></div><center>游戏屏幕中的不同 views</center>

<br>

如你所见，我将占位符放的 labels 里放入一些值（例如，“999999”）。这使得你更容易看到这些 labels 如何适应在屏幕上，当他们实际开始运作时。分数 label 可能具有很大的值，所以你最好确保 labels 有足够的空间来显示相应的值（例如分数）。

➤ 通过从 Object Library 中拖动各种 controls，试着自己来重现此屏幕。你需要几个新的 buttons，labels 和一个 slider。你可以在上面的截图中看到项目应该（大致）设置多大。如果你有一些小偏差，没关系。

要调整这些 views 的设置，请使用 **Attributes inspector**（属性检查器）。你可以在 Xcode 窗口右侧的窗格中找到此检查器：

<div align="center"><img alt="The Attributes inspector" src="http://imgur.com/dqfeAAG.png"/></div><center>The Attributes inspector</center>

<br>

Inspector 区域显示当前选择的项目的各个方面。例如，Attributes inspector 可以更改一个 label 的 background color 或 button上文本的大小。你已经看到显示一个 button's action 的Connections inspector。 随着你更熟练地使用 Interface Builder，你将使用所有这些 inspector 窗格来配置 views。

➤**（i）** button 实际上是常规 button，但他的**类型**在 Attributes inspector 中被设置为了 **Info Light**（信息灯）：

<div align="center"><img alt="button 类型允许您更改 button 的外观" src="http://imgur.com/2wgniuA.png"/></div><center>button 类型允许您更改 button 的外观</center>

<br>

➤ 同时使用 Attributes inspector 配置 **slider**。令其最小值应为 1，其最大值为 100，当前值为 50。

<div align="center"><img alt="滑块属性" src="http://imgur.com/6YhMP2y.png"/></div><center>滑块属性</center>

<br>

完成后，你的 scene 中应该有 12 个用户界面元素：一个 slider，三个 buttons 和一大堆 labels。很棒。

➤ 运行应用程序并玩上一分钟。这些 controls 并没有做太多的事情（除了应该弹出警报的那个 button），但你至少可以拖动 slider。

现在，你可以从待办事项列表中划掉更多的未完成事件了，所做的一切不需要任何编程！不过，好景不长，因为你将不得不写 Swift 代码来控制这些 controls 做任何事情你指定的事情。

## The slider

待办事项列表中的下一个项目是：“在用户按下 Hit Me button后，读取 slider 的值。”

如果在你看起来乱七八糟的 Interface Builder 中，你没有不小心将 button 与 showAlert action 断开连接，那么你就可以修改应用程序以在 alert 弹出窗口中显示 slider 的值。 （如果你断开了 showAlert 与 button 的关联，那么你应该先连接它。）

记住如何添加一个 action 到 view controller，以识别用户何时点击按钮？你可以为 Slider 做同样的事情。每当用户拖动 Slider 的旋钮时，都将执行这个新的 action。

添加这个 action 的步骤与你之前执行的步骤基本相同。

➤ 首先，转到 **ViewController.swift** 并在底部添加以下内容，只需要紧挨着最后一个括号：

```swift
@IBAction func sliderMoved(_ slider: UISlider) {
  print("The value of the slider is now: \(slider.value)")
}	
```

➤ 其次，转到 storyboard，按住 Ctrl 拖动 slider 到 Outline pane 中的 View Controller。放开鼠标按钮，从弹出窗口中选择 **sliderMoved: **。 完成！

只是为了刷新内存，Outline pane 位于 Interface Builder canvas 的左侧。它显示 storyboard 的 view 的层次结构。在这里你可以看到 View Controller 包含一个跨度有 scene 大小般的白色视图（简称为View），它又包含你添加的 sub-views（子视图）：buttons 和 labels。

<div align="center"><img alt="Outline pane 显示 storyboard 的 view 的层次结构" src="http://imgur.com/rmeKAL7.png"/></div><center>Outline pane 显示 storyboard 的 view 的层次结构</center>

<br>

请记住，如果你看不到 Outline pane，请单击底部的小图标以显示它：

<div align="center"><img alt="控制 Outline pane 显示或隐藏的按钮" src="http://imgur.com/ygdFlFs.png"/></div><center>控制 Outline pane 显示或隐藏的按钮</center>

<br>

连接 slider 时，确保按住 Ctrl 键拖动到 View Controller（带有黄色图标），而不是 View Controller Scene（灰色图标）。如果没有看到黄色图标，请单击 View Controller Scene 前的箭头将其展开。

如果一切顺利，sliderMoved: action 现在挂钩到滑块的 Value Changed 事件。 这意味着sliderMoved() method 将在每次用户向左或向右拖动 slider 时调用。

你可以通过选择 slider 并查看 **Connections inspector** 来验证是否已建立连接：

<div align="center"><img alt="该 slider 现在已经和 view controller 挂钩" src="http://imgur.com/bmvm8Xx.png"/></div><center>该 slider 现在已经和 view controller 挂钩</center>

<br>

<code class="highlighter-rouge"><strong>注意：</strong>你注意到 sliderMoved: action 在他的名称中有冒号，但 showAlert 却没有？这是因为 sliderMoved() 方法接受单个参数，slider，而 showAlert() 没有任何参数。如果操作方法有参数，Interface Builder 将向名称添加 : 。 往后你将了解更多关于使用参数的信息。</code>

➤ 运行应用程序并拖动 slider。

一旦开始拖动，Xcode 窗口就会在底部打开一个新窗格，所谓的 **Debug area**（调试区域），显示消息列表：

<div align="center"><img alt="在 Debug area 打印出信息" src="http://imgur.com/Xn6oM39.png"/></div><center>在 Debug area 打印出信息</center>

<br>

如果你向左滑动 slider，你应该看到值下降到 1 。一直向右，值应该会变成 100。

print() 函数是一个很好的帮助，告诉你在应用程序中发生了什么。它的整个目的是向 Debug area 写入一条文本消息。在这里，你使用它来验证你是否已正确地将 action 挂接到 slider，并且你可以在 slider 移动时读取其值。

我经常使用 print() 来确保我的应用程序运行正确如我所想，在我添加更多功能之前。将消息打印到 Debug area 既快速又容易。

<code class="highlighter-rouge"><strong>注意：</strong>你可能还会在 Debug area 看到一堆其他消息。这是来自 UIKit 和 iOS 模拟器的调试输出。你可以安全地忽略掉这些消息。</code>

## Strings（字符串）

要在你的应用程序中放置文本，你使用一个称为 “string” 的东西。 您目前使用过的 strings 有这些：

```swift
"Hello, World"
"This is my first app!"
"Awesome"
"The value of the slider is now: \(slider.value)"
```

前三个用于制作 UIAlertController；最后一个你使用在 print() 上面。

这样的文本块被称为 string，因为你可以将文本可视化为一个字符序列，就像它们是一个 string 上的珠子（对不起，它与衬衣（内衣）没有任何关系）：

<div align="center"><img alt="A string of characters" src="http://imgur.com/AQyfvcK.png"/></div><center>A string of characters</center>

<br>

与 strings 打交道是你在编写应用程序时必不可少的，所以在本教程系列的过程中，你会得到有关 strings 相当丰富的经验。

要创建一个 string，只需将文本放在双引号之间。在其他语言中，你也可以使用单引号，但在 Swift 中，它们必须是双引号。必须是半角的，不能使用全角。

总结：

```swift
// This is the proper way to make a Swift string:
"I am a good string"

// These are wrong（以下错误示范）:
'I should have double quotes'
''Two single quotes do not make a double quote''
“My quotes are too fancy”
@"I am an Objective-C string"
```

String 中的 \\(…) 之间的任何内容都是特殊的。print() 语句使用的 string 为 "The value of the slider is now: \\(slider.value)"。 想一下 \\(…) 作为占位符："The value of the slider is now: X"，其中 X 将被 slider 的值替换。

填空是在 Swift 中构建 string 的一种非常常见的方法。

## 引入 variables

在开发应用程序期间，使用 print() 将信息打印到 Debug area 中非常有用，但它对用户来说绝对没有用，因为他们看不到任何信息。

让我们改进此操作方法，并使其在 alert 弹出窗口中显示 slider 的值。 那么如何获得 slider 的值到 showAlert() ？

当你读取 sliderMoved() 中的 slider 的值时，那条 data 会消失（译者注：data 指 slider 的值，好比有一座图书馆，里面的书都没有名字，你想找你上次看过的那一本书），在 action method 结束时。如果你可以记住这个值并保存直到用户点击 Hie Me button 时，那将非常有用。

幸运的是，Swift 有一个构造块用于这个目的：变量。

➤ 打开 **ViewController.swift** 并在顶部添加以下内容，直接在下面行说 class ViewController:

```swift
var currentValue: Int = 0
```

你现在已向 view controller object 添加了名为 currentValue 的 variable。

代码应该看起来像这样（我省略了 method 的内部）：

```swift
import UIKit

class ViewController: UIViewController {
  var currentValue: Int = 0
  
  override func viewDidLoad() {
  ...
  }

  override func didReceiveMemoryWarning() {
  ...
  }

  @IBAction func showAlert() {
  ...
  }

  @IBAction func sliderMoved(_ slider: UISlider) {
  ...
  }
}
```

通常在 method 上面添加 variables，并使用制表符或两到四个空格缩进所有内容。你使用哪一个主要是个人喜好的问题。我喜欢使用两个空格。（你可以在 Xcode 的 preference（首选项）面板中进行配置。从菜单栏中选择 Xcode → preference… → Text Editing（文本编辑），然后转到 Indentation（缩进）选项卡。

记住，当我说一个 view controller，或任何 object，可以有 data 和 functionality，确实如此吗？ showAlert() 和 sliderMoved() actions 是 functionality 的示例，而 currentValue variable 是其 data 的一部分。

一个 variable 允许应用程序记住事物。将 variable 视为单个 data 的临时存储容器。有各种各样的容器和大小，就像 data 有各种形状和大小。

你不只是把东西放在容器中，然后忘记它。你将经常用新的值替换其内容。当你的应用需要记住东西的变化，就好像你把箱子打开把旧值拿出来，并放入新的值。

这是 variables 的整体观点：它们可以变化。例如，每次移动 slider 时，都将使用 slider 的新位置更新 currentValue。

存储容器的大小和 variables 可记住的值的类型由其 *data type*（数据类型）或只是 *type*（类型）决定。

你为 currentValue variable 指定了 type Int，这意味着此容器可以保存 20 亿到 -20 亿之间的整数（也称为 “integers”）。Int 是最常见的 data types 之一，但还有很多其他的，你甚至可以自己构造一个出来。

Variables 就像儿童的积木玩具：

<div align="center"><img alt="Variables 是容纳值的容器" src="http://imgur.com/ZKTrOpv.png"/></div><center>Variables 是容纳值的容器</center>

<br>

想法是把正确的形状放在正确的容器中。容器是 variable，它的 type 决定了什么 “形状”。 形状是可能的值它可以放入变量。

你可以稍后更改每个框的内容。例如，你可以取出蓝色正方形，并放入一个红色正方形，只要都是正方形。

但是你不能在圆孔中放一个正方形：值的 data type 和 variable 的 data type 必须匹配。

我说一个 variable 是一个临时存储容器。它会把内容保留多长时间？与肉类或蔬菜不同，如果你保持它们太长时间，variables 不会腐烂变坏——一个 variable 将无限期地保持它的值，直到你把一个新的值放入该 variable，或者直到你完全销毁容器。

每个 variable 都有一定的生命周期（也称为范围），它取决于程序中定义该 variable 的确切位置。在这种情况下，currentValue 会和它的所有者 ViewController 拥有一样的生命周期。他们的命运是交织在一起的（译者注：好比一根绳上的蚂蚱）。

讲了够多的理论了，让我们动手来做，让这个 variable 为我们工作。

➤ 将 **ViewController.swift** 中的 sliderMoved() method 的内容更改为以下内容：

```swift
@IBAction func sliderMoved(_ slider: UISlider) {
  currentValue = lroundf(slider.value)
}
```

你删除了print() 语句，并将其替换为此行：

```swift
currentValue = lroundf(slider.value)
```

这里发生了什么？

你已经看到 slider.value 之前，这是在那一刻 slider 的位置。这是介于 1 和 100 之间的值，可能带有小数点后面的数字。currentValue 是你刚刚创建的 variable 的名称。

要将新值放入 varibale，你只需这样做：

```swift
 variable = the new value
 译者注：变量 = 新值
```

这被称为 “assignment”（赋值）。将新值分配给 variable。相当于把形状放在盒子里这一步骤。这里，将代表 slider 位置的值放入 currentValue variable 中。

非常简单，但什么是 lroundf ？回想一下 slider 的值可以有小数点后面的数字。在移动 slider 时，你在 Debug area 中看到了 print() 的输出。

然而，如果你让玩家根据滑块的位置猜测一个这么精确带有这么多小数点的值，这个游戏会很难。这几乎不可能得到正确答案！

使用整数更公平。这就是为什么 currentValue 有 data type Int，因为该 type 存储 *integers*。integers 这个名词是整数的专用术语。

你使用 function lroundf() 将十进制数舍入到最接近的整数，然后将该四舍五入的数字存储到 currentValue 中。

<code class="highlighter-rouge"><strong>Functions 和 methods</strong></code>

`你已经看到 methods 提供了 functionality，但是 function 是将 functionality 放入你的应用程序的另一种方式。Functions 和 methods 是 Swift 程序实现将多行代码组合成单个且连贯的单元的功臣。`

`两者之间的区别是，一个 function 不属于一个 object，而一个 method 属于一个 object 换句话说，一个 method 就像一个 function——这就是为什么你使用 func 关键字来定义它们——除了你需要一个 object 来使用该 method。 但是因为 methods 有时被称为常规 functions 或 free functions（自由函数），可以在任何地方使用。`

`Swift 为你的程序提供了一个有用的函数库。function lroundf() 是其中的一个，你将在本课中使用其他几个。print() 也是一个 function，顺便说一下。你可以这么说，因为函数名称后面总是可能包含一个或多个参数的圆括号。`

---

译者注：

如果你被 methods 和 function 搞的晕头转向，试着把它们理解为动词和非谓语动词。它们这很相似却又那么的不同。不过暂时不理解这个问题也不大，没有专门的考试会考你怎么区分，只要你会使用它们即可。相信你以后会有一套自己的理解，本来就是人为规定的东西。

以下来自网上一些较权威说法：

**第一种：**

函数是一段代码，通过名字来进行调用。它能将一些数据（参数）传递进去进行处理，然后返回一些数据（返回值），也可以没有返回值。

所有传递给函数的数据都是显式传递的。

方法也是一段代码，也通过名字来进行调用，但它跟一个对象相关联。方法和函数大致上是相同的，但有两个主要的不同之处：

1. 方法中的数据是隐式传递的；
2. 方法可以操作类内部的数据（请记住，对象是类的实例化–类定义了一个数据类型，而对象是该数据类型的一个实例化）

[原文地址](http://stackoverflow.com/questions/155609/difference-between-a-method-and-a-function?rq=1)，这是 stackoverflow 上票数最高的答案（别问我什么是 stackoverflow）。

**第二种：**

方法和对象相关；

函数和对象无关。

Java 中只有方法，C 中只有函数，而 C++ 里取决于是否在类中。

---

➤ 现在将 showAlert() method 更改为以下内容：

```swift
@IBAction func showAlert() {
  let message = "The value of the slider is: \(currentValue)"
  
  let alert = UIAlertController(title: "Hello, World",
                                message: message,	// changed
                                preferredStyle: .alert)
                                
  let action = UIAlertAction(title: "OK",	// changed
                             style: .default, handler: nil)
    
  alert.addAction(action)
  
  present(alert, animated: true, completion: nil)
}
```
let message = 的行是新的。还要注意另外两个小的变化。

和以前一样，你创建和显示一个 UIAlertController，除了这个时候它的消息说：“The value of the slider is: X”，其中 X 被 currentValue variable 的内容（1 和 100 之间的整数）所替换。

假设 currentValue 是34，这意味着 slider 大约是左边三分之一。上面的新代码将 string "The value of the slider is: \ (currentValue)" 转换为 "The value of the slider is: 34"，并将其放入一个名为 message 的新 object 中。

旧的 print() 执行类似的操作，只是它将结果打印到 Debug area。但是，在此处，你不希望打印结果，而是在 alert 弹出窗口中显示结果。这就是为什么你告诉 UIAlertController 它现在应该使用这个新的 string 作为消息显示。

➤ 运行应用程序，拖动 slider，然后按 button。现在 alert 应该显示 slider 的实际值。

<div align="center"><img alt="The alert 显示 slider 的值" src="http://imgur.com/JcJZl6q.png"/></div><center>The alert 显示 slider 的值</center>

<br>

酷。你已经使用一个 variable，currentValue 来记住特定的 data 片段，slider 的四舍五入位置，以便它可以在应用程序的其他位置使用，在本例的情况下就是应用于 alert 的消息文本中。

如果你再次点按 button 而不移动 slider，则 alert 仍将显示相同的值。variable 保持其值，直到你把一个新的 variable 放进去。

## 你的第一个 bug（漏洞）

这里有一个小问题存在于应用程序中，虽然。也许你已经注意到了。让我们重现一下这个问题现场：

➤ 在 Xcode 中按停止按钮以完全终止应用程序，然后再次按运行。在不移动 slider 的情况下，立即按下 Hit Me button。

The alert 现在说：“The value of the slider is: 0”。 但是 slider 的旋钮显然在中心，所以应该显示的是 50。你发现了一个 bug！

**练习：**想想在这种特殊情况（启动应用程序，不要移动 slider，按下 button）下值为 0 的原因。

答案：这里的线索是，这只发生在你不移动 slider 的情况下。当然，在不移动 slider 的情况下，sliderMoved() 消息永远不会发送出去，并且永远不会将 slider 的值放入currentValue variable 中。

currentValue variable 的默认值为 0，就是你在此处看到的。

➤ 要修复此错误，请将 currentValue 的声明更改为：

```swift
var currentValue: Int = 50
```

现在，currentValue 的起始值是 50，它应该是与 slider 的初始位置相同的值。

➤ 再次运行应用程序，并验证该错误是否已解决。

你可以在本教程的源代码文件夹中的 **02 - Slider and Variables** 下找到应用程序的项目文件。

## 玩够了吧... 让我们做一个游戏！

你已经构建了用户界面，且知道如何找到 slider 的位置。这已经搞定了几个待办事项。

剩余下的一个大问题是生成目标的随机值，并计算玩家的效果。但首先，在 slider 上还有改进的地方。

## Outlets

你设法将 slider 的值存储到 variable 中，并将其显示在 alert 上。这很好，但你仍然可以改进一点。

如果你决定将 storyboard 中 slider 的初始值设置为 50 之外的其他值，如 1 或 100，该怎么办？那么 currentValue 会再次出错，因为应用程序总是假定它将在开始时为 50。你必须记住还修复代码以给 currentValue 一个新的初始值。

就我而言，这些小东西很难记住，特别是当项目变得更大，你有几十个 view controller 需要操心，或者你有几个星期没看你这些代码。

因此，为了一劳永逸地解决这个问题，你将在 **ViewController.swift** 中的 viewDidLoad() method 中做一些工作。该 method 目前看起来像这样：

```swift
override func viewDidLoad() {
  super.viewDidLoad()
  // Do any additional setup after loading the view, typically
	 from a nib. 
}
```

当你基于 Xcode 模板创建此项目时，Xcode 已经将 viewDidLoad() 方法放入源代码中。你现在将添加一些代码。

一旦 view controller 从 storyboard 文件加载其用户界面，viewDidLoad() 消息由 UIKit 发送。此时，view controller 还不可见，因此这是将实例 variables 设置为其正确初始值的好位置。

➤ 将 viewDidLoad() 更改为以下内容：

```swift
override func viewDidLoad() {
  super.viewDidLoad()
  currentValue = lroundf(slider.value)
}
```

这个想法是，你在 storyboard 中的 slider 上设置的任何值（无论是 50，1，100 还是其他），并使用它作为 currentValue 的初始内容。

回想一下，你需要舍入该数字，因为 currentValue 是一个Int，整数不能取小数点后面的数字。

不幸的是，当你按 Run 时，Xcode 抱怨这些更改。你可以亲自试试。

➤ 尝试运行应用程序。

Xcode 说 “Build Failed”，后面是类似：“Error: Use of unresolved identifier ‘slider’”（使用了未定义的 slider）。

这是因为 viewDidLoad() 不知道名为 slider 的任何东西。

那么为什么这个运行的更早，在sliderMoved() 里？ 让我们再看看那个 method：

```swift
@IBAction func sliderMoved(_ slider: UISlider) {
  currentValue = lroundf(slider.value)
}
```

这里你做同样的事情：你舍弃 slider.value 并把它放到 currentValue。那么为什么它在这里运行正常，而在 viewDidLoad() 出错？

区别是 slider 是 sliderMoved() method 中所谓的参数。参数是括号内的 method 名称后的内容。在这种情况下，有一个名为 slider 的参数，它引用发送此操作消息的 UISlider object。

Action methods 可以具有引用触发该 method 的 UI 控件的参数。当你希望在 method 中使用该 object 时，这就很方便的，就像你在这里所做的那样（所讨论的 object 是 UISlider）。

当用户移动 slider 时，UISlider object 基本上这样说： “Hey view controller, I’m a slider object and I just got moved. By the way, here’s my phone number so you can get in touch with me.”（嘿视图控制器，我是一个滑块对象，我刚刚移动。 顺便说一下，这里是我的电话号码，这样你可以与我联系）

slider 参数包含此 “phone number”（电话号码），但它仅在此特定 method 的有效期内有效。

换句话说，slider 是局部的; 你不能在任何其他地方使用它。

**Locals（本地）**

当我第一次引入 variables 时，我提到每个 variable 都有一定的生命周期，称为其范围。 variable 的范围取决于程序中定义该 variable 的位置。

Swift 有以下三个可能的范围级别：

1. **Global scope**（全局范围）。这些目标可以从任何地方访问。
2. **Instance scope**（实例范围）。这是说诸如 currentValue 这样的 variables。只要拥有它们的对象保持活动，这些它们就活着。
3. **Local scope**（本地范围）。具有局部作用域的 object（例如 sliderMoved() 的 slider 参数）仅在该 method 的持续时间内存在。只要程序的执行到离开这个 method，local objects（本地变量）就不再可访问。

让我们看看showAlert() 的顶部：

```swift
@IBAction func showAlert() {
  let message = "The value of the slider is: \(currentValue)"
  
  let alert = UIAlertController(title: "Hello, World",
                              message: message, preferredStyle: .alert)
                              
  let action = UIAlertAction(title: "OK", style: .default,
  ...
```

因为消息， alert 和 action objects 在方法内创建，所以它们是本地化。它们只有在执行 showAlert() action 时才存在，并在 action 完成时消失。

一旦 showAlert() method 完成，即当没有更多语句要执行时，计算机将销毁消息，alert 和 action objects。他们的存储空间将不再被需要。

然而，currentValue variable 永远存在... 或者至少只要 ViewController 存在（直到用户终止应用程序）。这种 type 的 variable 被命名为一个 instance variable，因为它的作用域与它所属的 object instance 的作用域相同。

换句话说，如果你想保持一个值，从一个动作事件到下一个动作事件，你应该使用 instance variables。

解决方案是将 slider 的引用存储为新的 instance variable，就像你对 currentValue 所做的一样。不过现在，variable 的 data type 不是 Int，而是 UISlider。你不使用常规的 intance variable，而是使用一个特殊的形式称为 *outlet*。

➤ 将以下行添加到 ViewController.swift：

```swift
@IBOutlet weak var slider: UISlider!
```

这一行放哪里不是很重要，只要它在类的 ViewController 的括号内的某处。我通常把 outlet 与其他 instance variables 放在一起。

这一行告诉 Interface Builder 你现在有一个名为 slider 的 variable，可以连接到 UISlider object。正如 Interface Builder 喜欢调用 method “actions”，它调用这些variable outlet。Interface Builder 不会看到任何其他 variables，只有标记为 @IBOutlet 的 variables。

不要担心感叹号和 weak 现在。为什么这些是必要的将在下面的教程中解释。现在只需记住一个 variable 的 outlet 需要声明为 @IBOutlet weak var，并在结尾有一个感叹号。（有时候你会看到一个问号，所有这些麻烦的问题会在适当的时候解释）

➤ 打开 storyboard。按住 Ctrl 并单击 slider。不要拖到任何地方只需要：放开鼠标按钮，弹出一个菜单，显示此 slider 的所有连接。（如果你不想按住Ctrl单击，也可以右键单击一次）

此弹出菜单的工作原理与 Connections inspector 完全相同。我只是想告诉你，它作为一种替代存在。

➤ 单击 **New Referencing Outlet** 旁边的空心圆，并拖动到 **View Controller**：

<div align="center"><img alt="连接 slider 到 outlet" src="http://imgur.com/2lsDipi.png"/></div><center>连接 slider 到 outlet</center>

<br>

➤ 在出现的弹出窗口中，选择 **slider**。

这是你刚刚添加到 object 的 outlet。你已成功将 slider object 从 storyboard 连接到 view controller 的slider outlet。

现在你已经完成了所有这些设置工作，你可以使用 slider variable 从 view controller 中的任何地方引用 slider object。

有了这些更改，就不再需要为 Interface Builder 中的 slider 手动设置初始值。 当应用程序启动时，currentValue 将始终对应于该设置。

➤ 运行应用程序并立即按下 button。它正确地说：“The value of the slider is: 50”。停止应用程序，进入 Interface Builder 并将 slider 的初始值更改为其他值，例如 25。再次运行应用程序，然后按下 button。 The alert 的文本消息现在应显示为 25。

当你完成游戏后，将滑块的起始位置恢复到 50。

**练习：**给 currentValue 一个初始值为 0。它的初始值不再重要——反正初始值将被 viewDidLoad() 重写， 但 Swift 要求所有 varibales 总是要有一些值（译者注：所有 variables 必须要被初始化），0 这个选择不错。

## Comments

你已经看到某些地方以绿色线条 // 作为开头几次了。这些是 comments。你可以在 // 符号后写任何你想要的文本，因为编译器会完全忽略这些行。（译者注：不同 IDE 或配色方案，对应的 comments color 不一样，不一定总是绿色的）

```swift
// I am a comment! You can type anything here.
```

/\* 和 */标记之间的任何内容也被视为 comments。// 和 /\* */之间的区别是前者仅在一行上起作用，而后者可以跨越多行。

```swift
/*
   I am a comment as well!（我同样也是一个 comment！）
   I can span multiple lines.（我可以跨越很多行。）
 */
```

/* */ 注释通常用于临时禁用源代码的整个部分，通常当你试图捕捉一个麻烦的 bug，这种做法被称为 “commenting out”。

comment 行的最佳用法是解释你的代码如何工作。编写出一个好的的源代码是不言自明的，但有时需要额外的说明是有用的。解释谁听？往往更多时候，是给自己看的。

除非你有一头大象的记忆，当你六个月后再看，你可能已经忘记了你的代码的工作原理。 使用注释来唤醒你的记忆。

正如你所看到的，Xcode 自动在源代码文件的顶部添加一个带有版权信息的 comment 块。就个人而言，我不在乎这些版权块。如果你不喜欢它们，随意删除那些行。

## 生成随机数

在游戏可玩之前，你还有很多方法去完善，所以让我们来看看待办列表中的下一个项目：生成一个随机数并在屏幕上显示它。

当你制作游戏时，随机数字很多，因为游戏需要有一些不可预测性。你不能真正地得到一个计算机生成真正随机和不可预测的数字，但你可以使用一个所谓的 pseudo-random generator（伪随机生成器）产生出这种 “随机” 数字。你将使用我最喜欢的一个 function，arc4random_uniform()。

生成这个随机数的好实际，是游戏开始的时候。

➤ 将以下行添加到 **ViewController.swift** 中的 viewDidLoad() 中：

```swift
targetValue = 1 + Int(arc4random_uniform(100))
```

完整的 viewDidLoad() 现在应该看起来像这样：

```swift
override func viewDidLoad() {
  super.viewDidLoad()
  currentValue = lroundf(slider.value)
  targetValue = 1 + Int(arc4random_uniform(100))
}
```

你在这里做了什么？首先，你使用了一个新的 variable targetValue。你还没有真正定义这个 variable，所以你必须马上做这件事。

你还调用 arc4random_uniform()  function 传递一个介于 0 和 100 之间的任意整数（整数）。

实际上，你将获得的最大数字是 99，因为 arc4random_uniform()  的结果不包含上限。它能达到100，而不是包括。要获取真正在 1 ～ 100 范围内的数字，你需要向 arc4random_uniform() 的结果加 1。

你仍然必须将 variable targetValue 添加到 view controller，否则 Xcode 会抱怨它不知道关于这个 variable 的任何信息。

如果你不告诉编译器 targetValue 是什么样的 variable（译者注：它的 type），那么它不知道要为它分配多少存储空间，也不能检查你是否在任何地方正确地使用这个变量。

➤ 在 **ViewController.swift** 的顶部添加新 variable，和其他 variables 放在一起：

```swift
var targetValue: Int = 0
```

Swift 中的 variables 必须总是有一个值，所以在这里你将它初始化为 0。不过它总是会被 viewDidLoad() 中的随机值覆盖。

<code class="highlighter-rouge"><strong>注意：</strong>直到你做出最新的更改之前，Xcode 可能已经指出，它不知道 targetValue variable 是什么。但是更改后该错误消息现在应该已经消失。</code>

`Xcode 试图帮助你，它会在你输入时分析程序错误。有时，当你完成所做的更改时，可能会看到临时警告和错误消息消失。`

`不要被这些信息吓唬到; 它们只是短暂的，因为代码处于变化状态（译者注：比如你正在写一个 function 还没来得及写花括号因为你才刚刚写到函数的名字，这时 Xcode 会报错）。`

我希望你很清楚设置 targetValue 这一个 instance variable 的原因。

你想在一个地方计算随机数——在 viewDidLoad()，然后记住它（保存它的值）在 showAlert() 中，直到用户点击 button。

➤ 将 showAlert() 更改为以下内容：

```swift
@IBAction func showAlert() {
  let message = "The value of the slider is: \(currentValue)" +
                "\nThe target value is: \(targetValue)"
                
  let alert = . . .
}
```

Tips：每当你看到 . . . 在源代码列表中，我想表达的意思就是：这部分没有改变。（千万不要把那里原有的内容替换为一些省略号！）

你只需将随机数（现在存储在 targetValue 中的值）添加到消息 string。这应该看起来很熟悉：\\(targetValue) 占位符替换为实际的随机数。

这里新出现了一个 \n 字符序列。它代表你想在那个点插入一个特殊的 “新行” 字符（译者注：就是所谓的换行），这将把文本分成两行，所以这让消息读起来更容易。

➤ 运行应用程序并尝试！

<div align="center"><img alt="The alert 在新的一行显示出目标值" src="http://imgur.com/gt4UmUy.png"/></div><center>The alert 在新的一行显示出目标值</center>

<br>

<code class="highlighter-rouge"><strong>注意：</strong>以前你已经使用 + 操作符将两个数字添加在一起（就像它在数学中的效果一样），但是在这里你还使用 + 将不同位的文本拼接成一个大的 string。</code>

`Swift 允许对不同的任务使用相同的操作符，具体取决于所涉及的数据类型。如果你有两个整数， + 就是求和。但是使用两个字符串，+ 将它们连接成一个较大的字符串。（译者注：运算符的重载）`

`编程语言通常使用相同的符号用于不同的目的，这取决于上下文。（因为只有这么些符号可以用）`

## 为游戏增加回合

如果你按几次 Hit Me button，你会注意到随机数从不改变。 恐怕游戏不会那么有趣。

发生这种情况是因为你在 viewDidLoad() 中生成了随机数，之后不再重复。 viewDidLoad() method 只在在应用程序启动期间 view controller 创建之时被调用一次。

待办事项列表上的项目实际上表示：“Generate a random number *at the start of each round*”（在每轮开始时生成一个随机数）。让我们来谈谈一个回合在游戏中的意义。

当游戏开始时，玩家的得分为 0，回合数为 1。你将 slider 设置为在中间（值为50）并计算随机数。然后等待玩家按下 Hit Me button。一旦她这样做，回合结束。

你计算这个回合的分数，并将它们添加到总分。然后你增加回合数并开始下一回合。你再次将 slider 重置到中间位置，并计算一个新的随机数。Lather，rinse，repeat（泡沫，冲洗，重复）。

---

译者注：**Lather，rinse，repeat**（有时是 **wash，rinse，repeat**）这是一个成语，引用了许多品牌的洗发水的说明。它也用作幽默的方式指出，如果这样的说明，如果采取字面意思会导致重复相同的步骤，无止境的循环，至少直到洗完用尽。它也是一个讽刺的隐喻，以下的指令或程序很盲目没有批判性思维。它被称为洗发剂算法，并且是介绍计算机科学类中的算法的经典示例。在 Benjamin Cheever 的小说 *The Plagiarist*（剽窃者） 中，虚构的广告主管通过在其说明中添加 “repeat” 一词来增加其客户与洗发水的销售量。上文中理解为反复做一件事即可。

---

每当你发现自己在思考：“在应用程序中的这一点，我们必须这样做”，那么它是有意义的，应该为其创建一个新的 method。这个方法将在自己的单元中很好地捕获该 functionality。

➤ 记住这一点，将以下新方法添加到 **ViewController.swift**。

```swift
func startNewRound() {
  targetValue = 1 + Int(arc4random_uniform(100))
  currentValue = 50
  slider.value = Float(currentValue)
}
```

你把它放在哪里并不重要，只要它在类 ViewController 的括号内，这样编译器知道它属于 ViewController 这个 object。

它与你之前做的没有很大的区别，除了你把设置一个新回合的逻辑移动到自己的 method startNewRound() 中。这样做的优点是，你可以在多个地方使用此逻辑。

首先，你将从 viewDidLoad() 调用此新方法来设置第一轮的所有内容。回想一下，viewDidLoad（） 只会在应用程序启动时发生一次，因此这是开始第一轮游戏的好起点。

➤ 将 viewDidLoad() 更改为：

```swift
override func viewDidLoad() {
  super.viewDidLoad()
  startNewRound()
}
```

注意，你已经从 viewDidLoad() 中删除了现有的语句，并且只是调用 startNewRound() 来替换它们。

在玩家按下 Hit Me button 后，从 showAlert() 中调用 startNewRound()。

➤ 对 showAlert() 进行以下更改：

```swift
@IBAction func showAlert() {
  ...
  startNewRound()
}
```

对 startNewRound() 的调用在最后，紧接着 present(alert, ...)。

到目前为止，UIKit 已经调用了 view controller 的 method：当应用程序加载时执行 viewDidLoad()，玩家点击 button 时执行 showAlert()，当玩家拖动 slider 时执行 sliderMoved()，等等。这是我们之前讨论的事件驱动模型。

它也可以手动调用 method，这是你在这里做的。你正在从 object 中的一个 method 发送消息到同一个 object 中的另一个 method。

在这种情况下，view controller 向其自身发送 startNewRound() 消息，以设置新轮次。然后 iPhone 将去那个 method 里并逐个执行它的语句。当 method 中没有更多的语句时，它返回到调用 method，并继续往下执行——如果这是第一次，则执行 viewDidLoad()，否则该执行的为每一回合的 showAlert()。

有时你可能会看到类似这样写的 method 调用：

```swift
self.startNewRound()
```

这与刚才没有 “self.” 的 startNewRound() 做完全相同的事情。回忆我刚才说的 view controller 发送消息给自己？那么，这就是 “self”（自我） 的意思。

调用你平时写的 object 的方法：

```swift
receiver.methodName(parameters)
//接收者.方法名(参数)
```

The receiver（接收者）是你发送消息的 object。如果你发送消息给自己，那么接收者是自己。但是因为向自己发送消息是很常见的，所以你也可以丢掉这个特殊的关键字（译者注：这里指 self）。

老实说，这不是你第一次调用 method。addAction() 是 UIAlertController 上的一个方法，present() 是所有 view controller 都有的 method，包括你的。

当你写 Swift 程序时，你所做的很多事情是调用 object 的 method，因为这是你的应用程序中的 object 的沟通方式。

我希望你能了解把 “new round”（新回合）逻辑放到它自己的 method 中的优点。如果你不这么做，viewDidLoad() 和 showAlert() 的代码如下所示：

```swift
override func viewDidLoad() {
  super.viewDidLoad()
  
  targetValue = 1 + Int(arc4random_uniform(100))
  currentValue = 50
  slider.value = Float(currentValue)
}
@IBAction func showAlert() { 
  ...
  
  targetValue = 1 + Int(arc4random_uniform(100))
  currentValue = 50
  slider.value = Float(currentValue)
}
```

你能看到这里发生了什么吗？相同的功能在两个地方重复。当然，在这里只有三行，但往往真实情况中你不得不重复的代码会更多。

如果你决定改变这个逻辑，会怎么样？你就必须在两个地方做这个更改。

如果你最近写了这段代码，但是如果你必须在几个星期之内做出这样的修改（译者注：前一句提到的修改逻辑），你可能可以记住这样做，但是你更可能只在一个地方更新它并忘记了另一个。

代码重复是一个很大的错误来源，所以如果你需要在两个不同的地方做同样的事情，考虑为它写一个新的 method。

method 的名称也有助于说明它应该做什么。你可以一眼就知道以下内容是什么吗？（译者注：英文不好的同学可能就有点麻烦了）

```swift
targetValue = 1 + Int(arc4random_uniform(100))
currentValue = 50
slider.value = Float(currentValue)
//目标值 = 1 + 转换为整形(arc4random_uniform(100))
//当前值 = 50
//滑块.值 = 转换浮点型的(当前值)
//你可以很清楚的了解到，这三句话就是在计算一个新的随机数，并把滑块位置恢复到中间
```

你大概会有理由这样想：“It is calculating a new random number and then resets the position of the slider, so I guess it must be the start of a new round.”（计算新随机数，恢复滑块位置，开始新回合）

一些程序员将使用 comment 来记录发生了什么，但在我的看法是，这样表达更清楚：

```swift
startNewRound()
//开始新回合（）
```

这行几乎说明了你会做什么。如果你想知道在新一轮中发生了什么的细节，你总是可以查找 startNewRound() method 并查看它的内部代码。

编写的好的源代码本身就是对自己的一个说明，让人一读就懂甚至不需要 comments。我希望我已经说服你认同这样构建新 method 的价值！

➤ 运行应用程序，并确认在每次轻击 button 后程序会计算 1 到 100 之间的新随机数。

你也应该注意到，每个回合后，slider 重置到中间位置。这是因为 startNewRound() 将 currentValue 设置为 50，然后告诉 slider 去该位置。这与你之前做的相反（你曾经读取 slider 的位置并把它放到 currentValue 中），但是我认为如果你在每个回合中从相同的位置开始，这样游戏效果更好。

**练习：**只是为了好玩，修改代码，当新回合开始时，slider 不会重置到正中间。

顺便说一下，你可能想了解一下 Float(…) 和 Int(…) 它们在下面这些行出现过：

```swift
targetValue = 1 + Int(arc4random_uniform(100))
slider.value = Float(currentValue)
```

Swift 是一种所谓的 *strongly typed*（强类型）语言，意味着它是非常挑剔形状，你不能把不同的形状放到同一个盒子中。例如，如果一个 variable 是一个Int，你不能把一个 Float 的值放入进去，反之亦然。

UISlider 的值恰好是一个 Float，它是一个数字，小数点后面有数字——之前你在打印出 slider 的值时看到了这一点，但 currentValue 是一个 Int。 所以这样赋值是错的：

```swift
slider.value = currentValue
```

编译器认为这是一个错误。但是有些编程语言很乐意将 Int 转换为 Float，但 Swift 希望你明确指出这样的转换。

当你说 Float(currentValue) 时，编译器获取存储在 currentValue 框中的 integer，并将其放入一个新的 Float 值，它可以赋给 UISlider。

类似的事情发生在 arc4random_uniform()，其中随机数在被放入 targetValue 之前被转换为 Int。

因为 Swift 和大多数其他编程语言比起来对待这种事情的时候更严格，所以对于语言新手来说，它往往是一个困扰的来源。不幸的是，Swift 的错误信息并不总是能够很清楚的说明代码哪部分是错误的并且为什么。

只要记住，如果你得到一个错误消息，“cannot assign value of type 'something' to type 'something else'”（不能分配 ”XXX“ 类型的值给 ”WWW“ 类型），那么说明你试图混合不兼容的数据类型。解决方案是将一个类型显式转换为另一个类型，就像你在这里做的一样。

## 将目标值放入 label

很好，你想出了如何计算随机数以及如何将它存储在一个 instance variable：targetValue 中，以便以后可以访问它。

现在你要在屏幕上显示目标值。没有它，玩家不会知道要往哪里瞄准，这将使得游戏几乎不可能获胜...

当你制作 storyboard 时，你已经为目标值添加了 label（右上角）。诀窍是把 targetValue  variable 的值放入这个 label。要做到这一点，你需要完成两件事：

1. 为 label 创建 outlet，以便你可以发送消息
2. 给 label 显示新的文本

这将非常类似于你对 slider 做的事情。回想一下，你添加了一个 @IBOutlet variable，以便可以在 view controller 中的任意位置引用 slider。使用此 outlet variable，你可以通过 slider.value 请求获取 slider 的值。你会为 label 做同样的事情。

➤ 在 **ViewController.swift** 中，在其他 outlet 下面添加以下行：

```swift
@IBOutlet weak var targetLabel: UILabel!
```

➤ 在 **Main.storyboard** 中，单击以选择 label（顶部的说明为 “100” 的 label）。

➤ 转到 **Connections inspector**，然后从 **New Referencing Outlet** 拖动到 **View Controller**。

<div align="center"><img alt="将目标值 label 连接到其 outlet" src="http://imgur.com/aD2n32x.png"/></div><center>将目标值 label 连接到其 outlet</center>

<br>

➤ 从弹出窗口中选择 **targetLabel**，以完成连关联。

➤ 让新的目标址 label 上显示出来，在 startNewRound() 下面添加以下方法到 **ViewController.swift**：

你把这个逻辑放到它自己的 method 中，因为你可能会从不同的地方使用它。

Method 的名称可以清楚表明它的作用：它更新 label 的内容（updateLabels）。目前它只是设置单个 label 的文本，但后来你将添加代码来更新其他 label（总分，回合数）。

updateLabels() 中的代码现在对你来说应该没有什么新奇的地方，虽然你可能想知道为什么这样写，明明这样更简单：

```swift
targetLabel.text = targetValue
```

答案是，你不能把一种 data type 的值放入另一种 type 的 variable 中去。方形钉不适合圆孔。（译者注：好比手套穿脚上，袜子戴手上）

The targetLabel outlet 引用一个 UILabel object。UILabel object 具有一个 text 属性，它是一个 string object。你只能把 string 的值放入文本，但上面那行代码试图把 targetValue 放进去，它是一个 Int。这不可能成功，因为一个 Int 和一个 string 是两种非常不同的东西（type）。

所以你必须将 Int 转换为 string，这就是 String(targetValue) 的作用。它类似于你之前见过的 Float(…) 和 Int(…)。

我猜到你想这样说：你也可以把它写成一个 string 和一个像以前一样的占位符：

```swift
targetLabel.text = "\(targetValue)"
```

你最喜欢用哪种方法只不过是你个人口味的问题。任何一种方法都会正常工作。

请注意，updateLabels() 是一个常规 method——它不作为 action 附加到任何 UI controls 上，因此它不会做任何事情，直到你实际调用它。（你懂的，因为它没有在任何地方说 @IBAction）

调用 updateLabels() 的逻辑位置将在每次调用 startNewRound() 之后，因为这是你计算新目标值的地方。

目前，你从两个地方发送 startNewRound() 消息：viewDidLoad() 和 showAlert()，让我们更新这些 method。

➤将 viewDidLoad() 和 showAlert() 更改为：

```Swift
override func viewDidLoad() {
  super.viewDidLoad()
  startNewRound()
  updateLabels()      // add this line
}
```

```Swift
@IBAction func showAlert() {
  ...
  
  startNewRound()
  updateLabels()      // add this line
}
```

你应该只用键入 method 名称的前几个字母，**upd**，Xcode 将自动补齐其余的。按 **Enter** 接受建议：

<div align="center"><img alt="Xcode 自动补全提供的建议" src="http://imgur.com/r5EpyMK.png"/></div><center>Xcode 自动补全提供的建议</center>

<br>

➤ 运行应用程序，你实际上将在屏幕上看到随机值。这应该使它更容易被瞄准，能让玩家看到目标。

<div align="center"><img alt="右上角的 label 现在显示随机值" src="http://imgur.com/MnbwGKa.png"/></div><center>右上角的 label 现在显示随机值</center>

<br>

你可以在本教程的源代码文件夹中的 **03 - Outlets** 下找到应用程序的项目文件。

**Action methods vs. normal methods**

那么 action method 和常规 method 之间的区别是什么？

答：没有。

一个 action method 和其他 method 一样。唯一特别的地方是 @IBAction 说明符。这允许 Interface Builder 查看 method，以便你可以将其连接到 button，button 等。

其他 method，如 viewDidLoad() ，没有 @IBAction 说明符。这是一件好事，因为如果你把这样的 method 挂钩到你的 button，会发生各种混乱。

这是一个 action method 的简单形式：

```swift
@IBAction func showAlert()
```

你还可以使用参数来请求对引发此操作的 object 的引用：

```swift
@IBAction func sliderMoved(_ slider: UISlider)
@IBAction func buttonTapped(_ button: UIButton)
```

但是以下 method 不能用作 Interface Builder 中的 action：

```swift
func updateLabels()
```

它没有被标记为 @IBAction，因此 Interface Builder 看不到它。使用 updateLabels()，你必须自己调用它。

如果你做得很远，那么我猜你喜欢你在读什么。 :-)

---

译者注：以下为原作者的一个小广告，有能力支持的可以购买原版，鼓励作者继续分享更多更好的经验。觉得啰嗦的可以跳过到下一条分割线之后。

这只是我的书 *The iOS Apprentice* 中的第一个教程：*Beginning iOS Development with Swift*（使用 Swift 开始 iOS 开发）。完整的书还有多三个像这样的大型教程——在每个教程中你都将从头开始打造一个完整的应用程序。

教程由浅入深。每个新的应用程序都比前一个更高级和复杂。这些应用涵盖了你需要知道的大部分知识，以制作自己的应用程序。

在系列的结尾，你会学到 Swift 和 iOS SDK 的基本要素。更重要的是，你应该对所有不同的部分如何组合在一起有更好的理解，以及如何解决问题，就像专业开发人员一样。

我有信心，通过这些教程，你将能够自己独立的把你的想法变成真正的应用程序！

<div align="center"><img alt="" src="http://imgur.com/V3PbusK.png"/></div>

<br>

你可能不知道一切，但你将能成为独当一面的开发人员——而且你会准备好畅游在令人兴奋的 iPhone 和 iPad 开发的世界。

*The iOS Apprentice* 会教你的一些亮点：

- **如何在 Swift 中编程**，即使你从来没有编程过或害怕学习一门新语言。
- **如何像一个程序员一样思考**。你不仅仅是一个 code monkey（码农？），只是把源代码插入编辑器。作为一个程序员，你必须考虑困难的计算问题，并找到创造性的解决方案。一旦你拥有这个宝贵的技能，你可以编程任何东西！
- **使用 SDK 的经验**。iOS SDK 是巨大的，我们没有办法去了解一切，但我们并不需要了解全部。你只需要掌握基本的构建块，像是 view controllers 和 table views。你还将学习如何使用来自你的应用程序的 Web 服务以及如何制作 iPad 应用程序。一旦你理解了这些基本原理，你可以很容易地通过自己学习 SDK 的其余部分工作的原理。
- **如何使应用程序的外观和给人的感觉变得更好**。在这个过程中，不仅仅是编程。我们将讨论用户界面设计以及图形和动画技术。当你给游戏一个改造和添加支持不同的 iPhone 模型，显然你已经体验过了这件事。
- **最新和最棒的**。我们将充分利用 Swift 和最新的 iOS 功能，如汽车布局和通用 storyboard。教你如何使用 iOS 开发的旧方法是没有意义的，有很多书在编写的时候是最新的，但现在已经过时了。每一个新版本的 iOS 都增加了改进的开发技术，你将会使用这些帮助你更好的进行开发。

这不仅是一堆干的理论，而是实践的实践建议！我会解释一下，当你在做真正的应用程序的一切工作，有大量的图片，清楚地说明了正在发生什么。

如果这个点子听起来非常有趣，请跳到 [raywenderlich.com/store/ios- apprentice](raywenderlich.com/store/ios- apprentice) 获得完整的 *iOS Apprentice* 系列。

---

## 计算得分

现在你既有目标值（随机数）和读取 slider 的位置的 method，你可以计算玩家得分的点数。

The slider 越靠近目标，玩家的点数越高。

要计算这个回合的分数，请看看 slider 的值与目标之间的距离：

<div align="center"><img alt="计算 slider 位置和目标值之间的差值" src="http://imgur.com/Mlyg86t.png"/></div><center>计算 slider 位置和目标值之间的差值</center>

<br>

找到目标和 slider 之间的距离的简单方法就是用 targetValue 减去 currentValue。

不幸的是，如果 slider 位于目标的右边，则得出负值，因为现在的 currentValue 大于 targetValue。

你需要一些方法把负距离变成正值——或者你最终从玩家的分数中减去点数（这样未免不公平）。

如果总是做减法后取相反数 -(currentValue - targetValue)——这并不会解决问题，因为如果 slider 位于目标的左侧而不是右侧，则差值将为负值。

嗯，看起来我们在这陷入了麻烦...

**练习：**如果我要求你用自然语言解决这个问题，你将如何设计这个问题的解决方案？不要担心如何用计算机语言表达现在，只是想到它在纯英语。（译者注：你可以用中文，重要的是思路）

我想出的思路像是这样：

- 如果 slider 的值大于目标值，则差值为： slider 值减去目标值。
- 但是，如果目标值大于 slider 值，则差值为：目标值减去 slider 值。
- 否则，两个值一定是相等的，那么差值为零。

为了得到一个恒为正数的值这总会导致一个差异，因为你总是从较大的数字中减去较小的数字。

来做一下数学计算：

如果 slider 于位置 60，目标值为 40，则屏幕上的 slider 位于目标值的右侧，差值为 60 - 40 = 20。

如果 slider 位置在 60，目标值为 40，则屏幕上的 slider 位于目标值的右侧，差值为 60 - 40 = 20。

**Algorithms**（算法）

你刚刚做的是想出一个 algorithm，这是一个花哨的术语，用于解决计算问题的一系列机械步骤。这只是一个非常简单的 algorithm，虽然这个比较简单但不可否认它就是一个 algorithm。

存在许多着名的 algorithms，诸如用于对项目列表进行排序的快速排序和用于通过这种排序列表快速搜索的二分搜索。其他人已经发明了许多 algorithms，你可以在自己的程序中使用，这样就可以帮你省去很多思考！

但是，在你写的所有程序中，你可能需要提出一些自己的 algorithms。有些是简单的，如上面的一个；但也有可能很难，可能会导致你在绝望中摆摆手。但这是编程的乐趣的一部分。（译者注：当你做出来后，就好像解出一道很难的数学题一样）

计算机科学的学术领域主要关注点是学习 algorithms 和找到更好的 algorithms。

你可以用简单的英语描述任何 algorithms（译者注：俗称的伪代码）。它只是一系列的步骤，你执行计算的东西。通常你可以在你的脑海里或纸上，执行计算。但对于更复杂的算法，可能你永远也算不出，所以在某些时候，你必须将 algorithm 转换为计算机代码，让计算机强大的运算能力来帮你算出来。

我想要说的重点就是：如果你遇到困难，你不知道如何让你的程序计算一些东西，拿一张纸，并试着用英语写出步骤（译者注：咱们还是用中文吧）。暂时先把计算机放在一边，想想步骤。如何用手执行此计算？

有可能你想出了一个不同的方式来解决这个小问题，我会给你两个备选方案，但让我们先将它转换为计算机代码：

```swift
var difference: Int
if currentValue > targetValue {
  difference = currentValue - targetValue
} else if targetValue > currentValue {
  difference = targetValue - currentValue
} else {
  difference = 0
}
```

“if” 结构是新出现的。它允许你的代码做出决定，它的工作就像英语字面意思也有。一般来说，它的工作原理如下：

```swift
if something is true {
  then do this
} else if something else is true {
  then do that instead
} else {
  do something when neither of the above are true
}
//如果 某事 为 真 {
//	那么 执行 这个
//} 另外 如果 某事 为 真 {
//	那么 执行 这个
//} 如果以上都不符合 {
//	那么 做这件事
//}
```

你在 if 关键字后面加上一个所谓的 *logical condition*（逻辑条件）。如果该条件为 true（真），例如 currentValue 大于 targetValue，则执行 {} 括号之间的块中的代码。

然而，如果条件为 false（不为真），则计算机查看 else if 条件并对其进行计算。可能有不止一个，如果有，那么计算机久从顶部到底部一个接一个地尝试它们，直到一个被判断为 true。

如果没有发现条件有效，则执行 else 块中的代码。

在这个小的 algorithm 实现中，你首先创建了一个名为 difference 的 local

variable 来保存结果。这将是一个正整数或零，因此Int将做：

```swift
var difference: Int
```

然后，将 currentValue 与 targetValue 进行比较。 首先你确定 currentValue 是否大于 targetValue：

```swift
if currentValue > targetValue {
```

\> 是大于运算符。如果 currentValue variable 中存储的值至少比 targetValue variable 中存储的值大，则 currentValue > targetValue 条件被判断为 true。在这种情况下，执行以下代码行：

```swift
difference = currentValue - targetValue
```

在这里，用 currentValue（较大的一个）减去 targetValue（较小的一个），并将差值存储在 differrnce variable 中。

注意我如何命名 variable，清楚地描述 variable 包含什么样的 data。 大多时候你会看到如下代码：

```swift
a = b - c
```

它不能立即清楚这是什么意思，除了让你知道这是一个减法运算。variable 名 “a”，“b” 和 “c” 这没有给出任何表明这些变量目的的提示。

回到 if 语句。如果 currentValue 等于或小于 targetValue，则条件为 false（或计算机为假），程序将跳过代码块直到达到下一个条件：

```swift
} else if targetValue > currentValue {
```

同样的事情在这里发生，只不过现在 targetValue 和 currentValue 的角色被颠倒了。当 targetValue 是两个值中的较大值时，计算机将只执行以下行：

```swift
difference = targetValue - currentValue
```

这次你用 targetValue 减去 currentValue（换句话说），并将结果存储在 difference variable 中。

还有最后一种情况，你还没有处理，就是 currentValue 和 targetValue 是相等的。如果发生这种情况，玩家将 slider 精确地放在随机数的位置，一个完美的分数。在这种情况下，差值为0：

```swift
} else {
  difference = 0
}
```

在这一点上，你已经确定一个值不大于另一个值，也不会更小，那么只剩下一个可能性：两数字相等。

➤ 让我们把这个 algorithms 添加到 action 中。将它添加到 showAlert() 的顶部：

```swift
@IBAction func showAlert() {
  var difference: Int
  if currentValue > targetValue {
    difference = currentValue - targetValue
  } else if targetValue > currentValue {
    difference = targetValue - currentValue
  } else {
    difference = 0
  }
  let message = "The value of the slider is: \(currentValue)"
            + "\nThe target value is: \(targetValue)"
  ... 
}
```

只是为了让你你可以看到它的工作原理，早些时候就已经让你添加 difference 的值到 alert 的消息中。

➤ 运行它并亲自查看一下。

<div align="center"><img alt="The alert 显示目标值和 slider 值之间的差值" src="http://imgur.com/q0dUR5L.png"/></div><center>The alert 显示目标值和 slider 值之间的差值</center>

<br>

## 计算差值的替代方案

我之前提到，还有其他方法来计算 currentValue 和 targetValue 之间的正数差值。上述 algorithm 运行良好，但它用了八行代码。我想我们可以想出一个更简单的方法，占用更少的行。

新 algorithm 如下：

1. 用目标值减去 slider 的值。
2. 如果结果是负数，则将其乘以 -1以使其为正数。

现在你不再避免计算出负数，因为计算机可以正常工作，虽然仍有可能计算出负数，但你只需把它变成一个正数。

**练习：**将此 algorithm 转换为源代码。提示：algorithm 的英语描述包含单词 “if” 和 “then”，这是一个很好的暗示，你必须使用 if 语句。

你应该得出像是这样的代码：

```swift
var difference = currentValue - targetValue
if difference < 0 {
  difference = difference * -1
}
```

这是一个非常直接的新 algorithm 的翻译。

你首先把两个 varible 做减法并将结果放入 difference variable 中。

请注意，你可以创建新 variable 并将计算结果分配给一行（译者注：声明时就定义）。你不需要把它放在两个不同的行，像这样：

```swift
var difference: Int
difference = currentValue - targetValue
```

此外，在新版本中，您不必告诉编译器，differece 需要 Int 值。因为 currentValue 和 targetValue 都是 Int，Swift是聪明的，能够推断出 difference 也应该是一个 Int。

这个特性称为 *type inference*（类型推理），它是 Swift 的主要卖点之一。

一旦得到减法结果，就使用 if 语句来确定差值是否为负，即小于零。如果是，则乘以 -1，并将新结果（现在为正数）返回到 difference variable。

当你写，

```swift
difference = difference * -1
```

计算机首先将差值乘以- 1。然后它把计算的结果重新区分。实际上，这将用正数覆盖 difference 的旧内容（负数）。

因为这是一个常见的事情（用变量本身加减乘除另一个数），所以有一个方便的捷径：

```swift
difference *= -1
```

\*= 运算符将 * 和 = 组合为一个新的操作符。最终结果是相同的：variable 的旧值已经消失，现在的结果为乘后的结果。

你也可以编写这个 algorithm 如下：

```swift
var difference = currentValue - targetValue
if difference < 0 {
  difference = -difference
}
```

而不是乘以 -1，现在使用 - 运算符，以确保 differenece 的值总是正的。这是因为 - 负数使它再次为正数。（问数学教授，如果你不相信我）

➤ 尝试使用这些新 algorithms。你应该替换 showAlert() 顶部的旧东西，如下所示：

```swift
@IBAction func showAlert() {
  var difference = currentValue - targetValue
  if difference < 0 {
    difference = difference * -1
  }
  
  let message = . . .
}
```

当你运行这个新版本的应用程序（试试！），它应该得到的结果完全一样的以前。计算的结果不会改变，改变的只是你所采用的技术。

关于这最后一个替代算法，我想告诉你来使用一个 function。

你已经看过 function 几次：你使用 arc4random_uniform() 当你做随机数字和 lroundf() 四舍五入 slider 的小数。

要确保数字始终为正，可以使用 abs() function。

如果你在学校学习数学，你可能会记得 “绝对值” 这个词，表示一个数字的值不考虑其符号。

这正是你在这里需要的，标准库包含一个方便的功能，它允许你将这个整个问题减少到一行：

```swift
let difference = abs(targetValue - currentValue)
```

无论是用 targetValue 减去 currentValue，还是反过来。如果数字为负数，abs() 将其变为正数。这是一个方便的 function，请记住。

➤ 对showAlert() 进行更改并尝试：

```swift
@IBAction func showAlert() {
  let difference = abs(targetValue - currentValue)
  
  let message = . . .
}
```

没有比这更简单的方法了！

**练习：**有个地方已经发生改变… 你能找到它吗？

答：你写的是 let differece，而不是 var difference 了。

Swift 区分了 variables 和所谓的 constants（常量）。与 variable 不同，constant 的值不能改变（你可能根据它的名称猜出）。

你只能把一些东西放到一个常数的盒子中，不能用其他东西代替。

关键字 var 创建一个 variable，而 let 创建一个 constant。这意味着 difference 现在是一个 constant，而不是一个 variable。

在以前的 algorithms 中，differnece 的值可能会改变。如果它是负面的，你把它变成正面。所需的 difference 是一个 variable，因为只有 variable 才能被分配新值。

现在你可以在一行中计算整个事情，diffeence 永远不会改变，一旦你给它一个值。在这种情况下，最好声明它为一个 constant。（为什么更好？它使你的意图清楚，同时又帮助 Swift 编译器更好地了解你的程序）

同样，消息，alert 和 action 也是 costant（一直都是！）。现在你知道为什么你使用 let 而不是 var 来声明这些 object 了吧。一旦他们获得了值，他们就不需要改变。

Constants 在 Swift 中非常常见。通常你只需要保持一个值很短的时间。如果在那个时间内值不会改变，最好声明它为一个 constant（let），而不是一个 variable（var）。

## 得分是多少？

现在你知道 slider 距离目标有多远，计算此轮的玩家得分变得十分容易。

➤ 将 showAlert() 更改为：

```swift
@IBAction func showAlert() {
  let difference = abs(targetValue - currentValue)
  let points = 100 - difference
  
  let message = "You scored \(points) points"
  ...
}
```

如果你把 slider 恰好放在目标上，差值为零，你可以得到的最大分数是100点。离目标越远，你赚取的积分就越少。

➤ 运行应用程序并自己玩玩看！

<div align="center"><img alt="The alert 显示当前回合的玩家的得分" src="http://imgur.com/D0mD0tC.png"/></div><center>The alert 显示当前回合的玩家的得分</center>

<br>

**练习：**因为 slider 的最大值为 100，最小值为 1，所以最大的区别是 100 - 1 = 99.这意味着你在一个回合中可以获得的绝对最差分数为1分。解释为什么会这样。 （Eek！它需要数学！）

## 跟踪玩家的总分

在这个游戏中，你想在屏幕上显示玩家的总分。每轮后，应用程序应该将新得分添加到总分，然后更新分数 label。

因为游戏需要保持总分在很长时间，你会把它放在一个 instance variable 中。

➤ 向 **ViewController.swift** 添加新的 score instance variable：

```swift
class ViewController: UIViewController {

  var currentValue: Int = 0
  var targetValue: Int = 0
  var score = 0              // add this line
```

嘿，这是什么？ 与其他两个 instance variable 不同，你没有说明得分是 Int。

如果你没有指定 data type，Swift 使用 *type inference* 来确定按照你的意思得到的是什么样的 type。因为 0 是一个整数，Swift 假定得分页应该是一个整数，因此自动给它 type Int。方便！

实际上，你不需要为其他 instance variable 指定 Int：

```swift
var currentValue = 0
var targetValue = 0
```

➤ 进行这些更改。 

多亏 type inference，你只需要列出数据类型的名称，即使你不给 variable 一个初始值。大多数时候，你可以安全地让 Swift 猜到类型。

我认为 type inference 是相当贴心！它肯定会帮你节省一些，呃，输入（还有其他地方）。

现在可以修改 showAlert() 以更新此分数 variable。

➤ 进行以下更改：

```swift
@IBAction func showAlert() {
  let difference = abs(targetValue - currentValue)
  let points = 100 - difference
  
  score += points        // add this line
  
  let message = "You scored \(points) points"
  ...
}
```

没有什么太令人惊讶的地方。你刚刚添加了以下行：

```swift
score += points
```

这将用户在这一回合中的得分加到总分。你也可以这样写：

```swift
score = score + points
```

就个人而言，我喜欢简写 += 版本，但任一个都没关系。两者完成完全相同的事情。

## 在屏幕上显示得分

你要做的事情与你为目标 label 做的完全相同：将分数 label 与一个 outlet 关联，并将分数值放入 label 的文本属性中。

**练习：**如果没有我的帮助，你是否可以做上述。你之前已经为目标值 label 执行了这些操作，因此你应该能够自己为总分 label 重复这些步骤。

你应该已经做了以下事情。将此行添加到 **ViewController.swift**：

```swift
@IBOutlet weak var scoreLabel: UILabel!
```

然后，你进入 storyboard，并将 label（写着 999999 的那个）连接到新的 scoreLabel outlet。

不确定如何连接 outlet？有几种方法可以将用户界面 object 连接到 view controller 的 outlet：

- Ctrl-单击 object 以获取上下文相关的弹出菜单。然后从 New Referencing Outlet 拖到 View Controller（你对 slider 做过同样的事情）。
- 转到 label 的 Connections Inspector 选项卡。从 New Referencing Outlet 到 View Controller（你对目标 label 做过同样的事情）。
- Ctrl - 从 View Controller 拖动到 label（现在尝试这个）。 确保你按照这个顺序；从 label 到 view controller的ctrl 拖动将不起作用。

There is more than one way to skin a cat（你总是可以找到不止一种方法来做某事），呃，连接 outlet。（译者注：就是有很多种方法将视图控制器中的对象和你的代码连接起来）

干得漂亮，这给了一个 scoreLabel 一个 outlet，你可以使用把文本放入 label。现在在代码中你应该做什么？在 updateLabels() 中。

➤ 返回 **ViewController.swift**，将 updateLabels() 更改为以下内容：

```swift
func updateLabels() {
  targetLabel.text = String(targetValue)
  scoreLabel.text = String(score)
}
```

没什么新鲜的。你将 score（一个 Int）转换为 string，然后将该 string 赋给 label 的 text 属性。为了对以上作出响应，label 将重新绘制自己与新的分数。

➤ 运行应用程序，并确认每次点击 button 时，此回合的积分都会添加到总分数 label 中。

<div align="center"><img alt="得分 label 记录玩家的总分" src="http://imgur.com/PnjlcPG.png"/></div><center>得分 label 记录玩家的总分</center>

<br>

## 更多的回合

说到回合，你还必须在每次玩家开始新回合时递增回合数。

**练习：**跟踪当前回合数（从 1 开始），并在新轮次开始时递增。在相应的 label 中显示当前轮数。到目前为止，如果你已经按照指示学习了之前的每一步，那么你已经可以自己完成这一部分，甚至你可以选择跳过这一小部分教程。祝你好运！

如果你猜到你必须添加另一个 instance variable，那么你是对的。你应该已经添加了以下行到源代码：

```swift
var round = 0
```

如果包括 data type 的名称，也可以，即使不做严格要求：

```swift
var round: Int = 0
```

还有 label 的 outlet：

```swift
@IBOutlet weak var roundLabel: UILabel!
```

和以前一样，你应该在 Interface Builder 中将 label 连接到此 outlet。

<code class="highlighter-rouge"><strong>不要忘记建立这些连接</strong></code>

`忘记在 Interface Builder 中建立连接是一个常常犯的错误，特别它真的发生在你身上了。`

`它经常发生像是我的家常便饭，我做一个 button 的 outlet，编写代码来处理该 button 上的点击，但是当我运行应用程序它不工作。通常它让我一些抓耳挠腮几分钟，然后意识到我忘了连接 button 到 outlet 或 action method。`

`你可以点击 button 然后按你的想法进行，前提是连接存在否则你的代码将不会响应。`

最后，updateLabels() 现在应该如下所示：

```swift
func updateLabels() {
  targetLabel.text = String(targetValue)
  scoreLabel.text = String(score)
  roundLabel.text = String(round)
}
```

你还能够弄清楚在哪里来增加 round variable？

我想说 startNewRound() method 是一个相当不错的地方。毕竟，当你开始一个新的回合，你调用这个 method。在那里增加回合计数器非常合理。

➤ 将 startNewRound() 更改为：

```swift
 func startNewRound() {
  round += 1           // add this line
  targetValue = 1 + Int(arc4random_uniform(100))
  currentValue = 50
  slider.value = Float(currentValue)
}
```

注意，当你声明 round instance variable 时，你给它一个默认值 0。因此，当应用程序启动时，round 最初是 0。当你第一次调用 startNewRound(0 时，它会添加 1 到这个初始 值，因此第一轮被正确计为回合 1。

➤ 运行应用程序并尝试。每当按下 Hit Me button 时，回合计数器应该更新。

<div align="center"><img alt="回合 label 计算已经进行了多少回合" src="http://imgur.com/VG3eZug.png"/></div><center>回合 label 计算已经进行了多少回合</center>

<br>

你可以在教程的源代码文件夹中的 **04 - Rounds and Score** 下找到应用程序的项目文件。 如果你遇到问题，比较你的应用程序版本与这些源文件，看看你是否遗漏了某些东西。

## 来给游戏润润色

你可以到此为止了，这已经是一个可玩的游戏了。游戏规则都是设定好的，逻辑也没有任何大的缺陷。据我所知，没有 bugs。但仍有一些改进的余地。

显然，游戏不是很漂亮，不过很快这将是你的关注点。同时，有一些较小的调整，需要你来做。

除非你已经改变它，否则 alert 的标题仍然说 “Hello, World!” 你可以替换为游戏名称，“Bull's Eye”，但我有一个更好的主意。如果你根据玩家的表现改变标题怎么办？

如果玩家将 slider 正好放在目标上，则 aliet 可以说：“完美！” 如果 slider 靠近目标但不在那里，则可以说：“你差不多了！”如果玩家离开 ，警报可以说：“差的有些远…” 等等。 这给玩家一个更多的反馈，他们表现的如何。

**练习：**想想一种方法来完成这个。你该把这个逻辑放在哪里，你怎么编程呢？提示：在前面类似情况的句子中你用了很多 “if”。

这个逻辑的正确位置是 showAlert()，因为这是创建 UIAlertController 的地方。你已经做了一些计算以构建消息文本，现在你会做类似的标题文本的东西。

➤ 下面是已更改的方法的全部内容：

```swift
@IBAction func showAlert() {
  let difference = abs(targetValue - currentValue)
  let points = 100 - difference
  score += points
  
  // add these lines
  let title: String
  if difference == 0 {
    title = "Perfect!"
  } else if difference < 5 {
    title = "You almost had it!"
  } else if difference < 10 {
    title = "Pretty good!"
  } else {
    title = "Not even close..."
  }
  
  let message = "You scored \(points) points"
  
  let alert = UIAlertController(title: title,	// change this
                                message: message,
                                preferredStyle: .alert)

  let action = UIAlertAction(title: "OK", style: .default, handler: nil)
  alert.addAction(action)
  present(alert, animated: true, completion: nil)
  
  startNewRound()
  updateLabels()
}
```

你新建一个名为 title 的 local string，其中将包含位于 alert 顶部的文本。最初，此标题没有任何值。

要决定使用哪种标题文本，要根据 slider 位置和目标值之间的差异：

- 如果它（差值）等于 0，那么玩家完全正确，你把文本 “Perfect!” 放到到标题里。
- 如果差值小于 5，则使用文本 “You almost had it!”。
- 小于 10 的差是 “Pretty good!”。
- 但是，如果差值为10或更大，那么显示 “Not even close…”。

你能遵循这里的逻辑吗？它只是一堆 if 语句，考虑不同的可能性，并选择一个 string 作为响应。

当创建 UIAlertController object 时，现在给它标题 string，而不是固定文本。

运行应用程序，玩一下。你会看到标题文字根据你的得分高低而变化。if 语句非常实用！

<div align="center"><img alt="带有新标题的 alert" src="http://imgur.com/qy4KifZ.png"/></div><center>带有新标题的 alert</center>

<br>

**练习：**当她为完美的得分时，给玩家额外 100 点奖励。这将鼓励玩家真正试图把 bull‘s eye 放在目标上。否则，完美得分 100 分和 98 或 95 分之间没有太大差异，会让玩家失去动力。

给玩家一点鼓励，尝试更努力——一个完美的得分不再只有 100，而是 200 分。你也可以给玩家 50 点，随你设置。

➤ 以下是我将进行这些更改的方式：

```swift
@IBAction func showAlert() {
  let difference = abs(targetValue - currentValue)
  var points = 100 - difference	// change let to var
  
  let title: String
  if difference == 0 {
    title = "Perfect!"	// add this line
    points += 100
  } else if difference < 5 {
    title = "You almost had it!"
    if difference == 1 {	// add these lines
      points += 50 
    }
  } else if difference < 10 {
      title = "Pretty good!"
  } else {
    title = "Not even close..."
  }
    
  score += points
  ... 
}
```

你应该注意到一些事情：

- 在第一个 if 你会看到一个大括号之间的新语句。当差值等于零时，你现在不仅将标题设置为 “Perfect!”，还可以额外获得 100 分。
- 第二个 if 改变了。现在有一个 if 里面有另一个 if。没有什么错！你想处理差异为 1 的情况，以给予玩家奖励积分。这发生在新的 if 语句内。毕竟，如果差值大于 0 但小于 5，它也可以是 1。因此，你执行额外的检查，以查看差异是否真的为 1，如果是，给玩家添加 50 分。
- 因为这些新的 if 语句添加额外的分，分数不能再是一个 constant；它现在需要是一个 variable。这就是为什么你把它从 let 改成 var。
- 最后，那一行 line score += points 已移动到 ifs 下面。这是必要的，因为应用程序可能更新这些 if 语句中的 points variable，并且你希望这些额外的也计入分数。

如果你做的有点不同，那也很好，只要它运作正常！通常有不止一种方法来编程某些东西，如果结果相同，则每种方式同样有效。

➤ 运行应用程序，看看是否可以得到一些奖励积分！

<div align="center"><img alt="恰好放在目标值上" src="http://imgur.com/Ki3mFOR.png"/></div><center>恰好放在目标值上</center>

<br>

**Local bariables 概述**

我想再次指出局部变量和实例变量之间的区别。 正如你现在应该知道的，局部变量只存在于定义它的方法的持续时间，而实例变量存在，只要视图控制器（拥有它的对象）存在。 同样的事情对于常量也是如此。

在 showAlert() 中，有六个 local variable，并且使用三个 instace variables：

```Swift
let difference = abs(targetValue - currentValue)
var points = 100 - difference
let title = . . .
score += points
let message = . . .
let alert = . . .
let action = . . .
```

**练习：**指出哪些是 local varables，哪些是 showAlert() method 中的 instance variables。在 local 中，哪些是 variables，哪些是 constant？

答案：Local variables 很容易识别，因为第一次在 method 中使用它们的名称前面有 let 或 var：

```swift
let difference = . . .
var points = . . .
let title = . . .
let message = . . .
let alert = . . .
let action = . . .
```

此语法创建一个新变量（var）或常量（let）。 因为这些 variables 和 constants 是在 method 内创建的，所以它们是 locals。

这六个项目——difference, points, title, message, alert, 和 action——仅限于 showAlert() method，并且不在其外部。一旦该 method 完成，本地的都不再存在。

例如，你可能会想知道，每当玩家点击 Hit Me button 时，difference 如何，即使它是一个 constant。constants 一旦给定一个值，以后不会改变？（译者注：提前透漏一下吧，就算是常量也是可以改变的。仔细看看前一句话，一旦 method 完成，本地的常量或者变量都不再存在。所以点击按钮后，又执行了一次方法，现在的那个常量已经不再是原来那个了。想象一下你有一支笔，笔芯已经没有墨水了，你把没水的笔芯丢掉然后换了一支新的笔芯进去）

这是为什么：每次调用一个方法时，都会重新创建其局部变量和常量。 旧的值早已被遗弃，你得到的是新的。

当调用 showAlert() 时，它会创建一个与前一个无关的完全新的 instance difference。这个特定的 constant 值只用到 showAlert() 结束，然后再次被遗弃。

下一次调用 showAlert() 之后，它会创建另一个新的 instance difference（以及其他 instances of locals points, title, message, alert 和 action）。等等… 有一些重要的回收在这里进行！

但是在 showAlert() 的单一调用中，difference 一旦具有其值就永远不会改变。唯一可以改变的地方是 points，因为它是一个 var。

另一方面，instance variables 在任何 method 之外定义。 通常将它们放在文件的顶部：

```swift
class ViewController: UIViewController {

  var currentValue = 0
  var targetValue = 0
  var score = 0
  var round = 0
```

因此，你可以从任何方法使用这些 variables，而无需再次声明它们，并且它们将保留其值。

如果你这样做，

```swift
@IBAction func showAlert() {
  let difference = abs(targetValue - currentValue)
  var points = 100 - difference
  
  var score = score + points       // doesn’t work!
  ...
}
```

然后他们不会和你预期一样的去工作。因为你现在把 var 放在 score 的前面，你已经使它成为一个新的 local variable，它只在这个 method 中有效。

换句话说，这不会向 *instance variable* 添加 points，而是添加到也被命名为 score 的新的 *local variable*。instance variable points 永远不会改变，即使它具有相同的名称。（译者注：经常会遇到本地变量和全局变量拥有相同名字，在 c++ 中 人们经常使用 this.a 表示全局变量 a，用 a 表示方法体内的本地变量 a。不过好习惯还是不要使用这么多重复的名字）

显然，这不是你想在这里发生。幸运的是，对于上面的代码上面甚至不会进行编译。Swift knows there’s something fishy about that line（知道上面这行代码有些蹊跷，猫腻）。

<code class="highlighter-rouge"><strong>注意：</strong>为了区分两种类型的 variables，使得方便且清楚地知道它们将存活多长时间，一些程序员在 instance variables 的名称前面加上下划线。</code>

`他们将命名 variable 为 _score而不是 score。现在看起来好多了，因为以下划线开头的名字不会被误认为是 locals。这只是一个惯例。Swift 不关心一种方式，也不关心你如何拼写你的实 instance variables。（译者注：就是不做硬性要求，无论你怎么命名都不会影响编译器的编译）`

`其他程序员使用不同的前缀，例如 “m”（member 成员）或 “f”（filed 字段）目的是一样的。有些甚至把下划线放在变量名后面。 疯狂！`

## 等待 alert 消失

关于这个游戏，有一些事让我困扰。你可能也注意到了...

一旦点击 Hit Me button，弹出 alert，slider 立即重置到其中心位置，回合数递增，目标值 label 获得新的随机数。

新的一回合已经开始，而你却正要观察的本回合的结果如何。这就很不方便而且容易造成混乱。

最好等待玩家关闭 alert 弹出窗口后才开始新的回合。只有这样，当前的轮才真正结束。

也许你想知道为什么这不是已经发生了？毕竟，在 showAlert() 中，只有在显示 alert 弹出窗口后才会调用 startNewRound()：

```swift
@IBAction func showAlert() {
  ...
  
  let alert = UIAlertController(. . .)
  let action = UIAlertAction(. . .)
  alert.addAction(action)
  
  // Here you make the alert visible:
  present(alert, animated: true, completion: nil)
  
  // Here you start the new round:
  startNewRound()
  updateLabels()
}
```

与你的预期可能相反，present(alert, …) 不阻止剩余的 method 继续执行，直到 alert 弹出窗口被关闭。这就是其他平台上的 alert 如何工作，而不是在 iOS 上。（译者注：会 javascript 的读者因该对这一点深有体会吧）

相反，present(alert, …) 将 alert 放在屏幕上并立即返回。showAlert() method 的其余部分杯立即执行，并且新的回合已经在 alert 弹出窗口这个动画完成之前开始。

用编程术语来讲，此处的 alert 是一个 work *asynchronously*（译者注：首先告诉你，synchronously 是同步的意思。没错，你很聪明 asynchronously 是异步的意思。单凭字面意思你应该了解了 alert 在 iOS 中是怎么工作了的吧）。关于这一点，在后面的教程中我会更多的讲述，但现在它对你意味着什么，因为在你预先不知道 alert 什么时候完成。但你可以打赌，在 showAlert() 之后运行一定没问题。

所以如果你不能在 showAlert() 中等待，直到弹出窗口被关闭，那么你怎么等待它关闭？

答案很简单：事件！正如你所看到的，iOS 的许多编程涉及等待特定事件发生——button 被点击，slider 被移动等等。这没有什么不同。你必须等待 “alert dismissed” 事件。同时，你什么都不需要做。

以下是它的工作原理：

对于 alert 上的每个 button，你必须提供一个 UIAlertAction object。此 object 告诉 alert 在 button 上的文本是什么——“OK”——button 的外观是怎么样的（你在这里使用默认样式）：

```swift
let action = UIAlertAction(title: "OK", style: .default, handler: nil)
```

第三个参数 handler，告诉 alert 该干什么当 button 被按下时。这是你一直在寻找的 “alert dismissed” 事件。

目前 handler 是nil，这意味着什么都没有发生。要改变这个，你需要给 UIAlertAction 添加一些源代码，当 button 被点击开始执行。当用户最终点击 OK 时，alert 将从屏幕中删除并跳转到你的代码。这是你的线索用它来搞定后面的事情。

这也称为 *callback* pattern（回调模式）。这种模式在 iOS 上显示有几种方式。通常，你将被要求创建一个新的 method 来处理事件。但在这里你会见识到新的东西：closure（闭包）。

➤ 将 showAlert() 的底部位更改为：

```swift
@IBAction func showAlert() {
  ...
  let alert = UIAlertController(. . .)
  
  let action = UIAlertAction(title: "OK", style: .default,
                             handler: { action in
                                         self.startNewRound()                           
                                         self.updateLabels()
                                      })
                                      
  alert.addAction(action)
  present(alert, animated: true, completion: nil)
}
```

这里发生了两件事：

1. 你从 method 底部删除对 startNewRound() 和 updateLabels() 的调用。（不要忘记这部分！）
2. 你把它们放在你给 UIAlertAction 的 handler 参数的一段代码中。

这样的代码块被称为一个 closure。你可以认为它是一个没有名字的 method。此代码不会立即执行，只有在轻击 OK button 时。此特定 closure 会通知应用程序启动新回合，并在 aliert 被关闭时更新 labels。

➤ 运行它并自己查看。我认为以这种方式游戏感觉好多了。

<code class="highlighter-rouge"><strong>Self</strong></code>

`你可能想知道为什么在处理程序块中你做了 self.startNewRound()，而不是像以前一样写startNewRound()。`

`self 关键字允许 view controller 引用自身。这不应该是一个奇怪概念。当你说，“我想要冰激凌”，你使用 “我” 一词来指自己。同样，object 也可以调用（谈论）自己。`

<code class="highlighter-rouge">通常，你不需要使用 self 向 view controller 发送消息，即使它被允许。异常：但是在 closure 中你<em>必须</em>使用 self 来引用 view controller。</code>

`这是 Swift 中的规矩。如果你忘记了一个 closure 中的 self，Xcode 不想构建你的应用程序（不信你试试）。这个规则之所以存在，因为 closure 可以 “capture”（捕获） variables，这带来了令人惊讶的副作用。你将在其他教程中了解更多。`

## 重新开始

不，这个项目从头到尾，你都不会离开源代码！我在谈论游戏的 “Start Over”（重新开始） button。此 button 应该重置得分，并让玩家回到第一回合。

Start Over button 的一个用途是用于对抗另一个人。第一个玩家做十轮，然后分数重置，第二个玩家做十轮。获得最高分的玩家获胜。

**练习：**尝试自己实现这个 Start Over button。你已经看到了如何使 view controller 对 button 按下做出反应，你应该能够找出如何更改得分和回合 variables。

你怎么做的？如果您遇到问题，请按照以下说明操作。

首先，向 **ViewController.swift** 添加一个 method 来启动一个新游戏。我建议
你把它放在 startNewRound() 附近，因为两者在概念上是相关的。（译者注：代码整洁，可读性是很重要的。除非你想辞职，可以改写一下，你走了以后这段代码就没人维护得了，几个月后就连自己都看不懂，以此报复老板。开玩笑的）

➤ 添加新 method：

```swift
func startNewGame() {
 score = 0
 round = 0
 startNewRound()
}
```

此 method 重置得分和回合数，并开始新回合。

注意你在这里设置 round 为 0，而不是 1。你使用 0，因为增加 round 的值是 startNewRound() 所做的第一件事。

如果你 将round 设置为 1，那么 startNewRound() 将向它加另一个 1 第一轮实际上将标记为第二轮。

所以你从 0 开始，让 startNewRound() 加一，一切都会正常工作。

（这应该说明为什么我们不用英语来编程）

你还需要一个 action method 来处理 Start Over button 上的敲击。

➤ 将 action method 添加到 **ViewController.swift**：

```swift
@IBAction func startOver() {
  startNewGame()
  updateLabels()
}
```

这并不重要，你放置这个方法的位置，但喝下面的其他动作方法放在一起是一个很好的主意。

当按下 Start Over button 时，startOver() action method 首先调用 startNewGame() 开始一个新游戏。（看，如果你选择有意义的 method 名称，然后阅读源代码真的不是那么难）

因为 startNewGame() 更改 instance variables 的内容，还调用 updateLabels() 来更新得分，回合和目标值 labels 的文本。

为了使事情保持一致，在 viewDidLoad() 中，你应该通过 startNewGame() 替换对 startNewRound() 的调用。因为得分和回合已经是 0 当应用程序启动时，它不会真正说明应用程序的工作原理，但它确实使源代码的意图更清楚。

➤ 进行此更改：

```swift
override func viewDidLoad() {
  super.viewDidLoad()
  startNewGame()        // this line changed
  updateLabels()
}
```

最后，你需要将 Start Over button 连接到 action method。

➤ 打开 storyboard，然后从 **Start Over **button Ctrl-拖动到 **View** **Controller**。放开鼠标，从弹出框中选择 startOver。将 button 的 Touch Up Inside 事件连接到你刚刚的定义的 action。

➤ 运行应用程序并玩几回合。按 Start Over，让你回到第一回合。

提示：如果你忘记了什么 button 或 label 连接到什么 method，你可以单击 storyboard 中的 **View Controller** 查看你到目前为止所有的连接。

你可以右键单击 View Controller 以获取弹出窗口，或者只需在 **Connections inspector** 中查看连接。这将显示已对 view controller 进行连接的所有连接。

<div align="center"><img alt="从 View Controller 到其他 objects 的所有连接" src="http://imgur.com/AMIPBAC.png"/></div><center>从 View Controller 到其他 objects 的所有连接</center>

<br>

你可以在教程的源代码文件夹中的 **05 - Polish** 下找到应用程序当前版本的项目文件。

## 添加关于屏幕

我希望到目前为止你不厌烦这个应用程序，因为还有一个功能，我想添加到它，一个 About（关于）屏幕，显示一些关于游戏的信息：

<div align="center"><img alt="新的 About 屏幕" src="http://imgur.com/QSc6hc4.png"/></div><center>新的 About 屏幕</center>

<br>

这个新屏幕包含一个所谓的 *text view*（文本视图）里面显示游戏规则和一个 button，让玩家关闭该屏幕。你通过点击游戏中的 (i) button 进入 About 屏幕。

大多数应用程序有多个屏幕，甚至非常简单的游戏，所以这是一个好时机，了解如何添加额外的屏幕到你的应用程序。

我已经指出了几次：你的应用程序中的每个屏幕都将有自己的 view controller。如果你认为 “screen”（屏幕） 是，“view controller” 也是。

Xcode 自动为你创建了主 ViewController object，但是 About屏幕的 view controller 就要你自己来创建了。

➤ 转到 Xcode 的 **File** 菜单，然后选择 **New → File…** 在弹出的窗口中，选择 **Cocoa Touch Class** 模板（如果你没有看到它，那么请确保在顶部选择 **iOS**）：

<div align="center"><img alt="选择 Cocoa Touch Class 的文件模板" src="http://imgur.com/7cPI336.png"/></div><center>选择 Cocoa Touch Class 的文件模板</center>

<br>

点击 **Next**。Xcode 给你一些选项来填写：

<div align="center"><img alt="新文件的选项" src="http://imgur.com/Fxx6744.png"/></div><center>保存新文件</center>

<br>

选择以下内容：

- Class: **AboutViewController**
- Subclass of: **UIViewController**
- Also create XIB file: Leave this box unchecked.
- Language: **Swift**

点击 **Next**。Xcode 会问你在哪里保存这个新的 view controller：

<div align="center"><img alt="保存新文件" src="http://imgur.com/aUkkJMt.png"/></div><center>新文件的选项</center>

<br>

➤ 选择 **BullsEye** 文件夹（此文件夹应已被选中）。

还要确保 **Group** 说 **BullsEye**，并在 list of **Targets**（目标列表）中的 BullsEye 前面有一个复选标记。（如果没有看到此面板，请单击 Options 按钮。）

➤ 单击 **Create** 完成。

Xcode 将创建一个新文件并将其添加到你的项目。你可能已经猜到的，新文件是 **AboutViewController.swift**。

<div align="center"><img alt="The project navigator 中的新文件" src="http://imgur.com/qE7b5gw.png"/></div><center>The project navigator 中的新文件</center>

<br>

要设计这个新的 view controller，你需要访问 Interface Builder。

➤ 打开 **Main.storyboard**。没有任何表示关于 view controller 的 scene，因此你必须先添加它。

➤ 从 **Object Librart** 中，选择 **View Controller** 并将其拖动到 main View Controller 右侧的 canvans 中。

<div align="center"><img alt="从 Object Library 中拖动新的 View Controller" src="http://imgur.com/xLNZtUP.png"/></div><center>从 Object Library 中拖动新的 View Controller</center>

<br>

这个新的 view controller 是完全空白的。你可能需要重新排列 storyboard，以使两个 view controller 不重叠。Interface Builder 并不总是非常整齐地摆放的东西。

➤ 将新 **Button** 拖动到屏幕中，并给它标题 **Close**。将它放在 vuew 底部中心的某个位置（使用蓝色指南线帮助定位）。

➤ 将一个 **Text View** 拖动到 view 中，使其覆盖 button 上方的大部分空间。

你可以在 Object Library 中找到这些组件。如果你不想滚动，可以通过在底部的字段中键入关键字来过滤组件：

<div align="center"><img alt="搜索文本组件" src="http://imgur.com/O0qActd.png"/></div><center>搜索文本组件</center>

<br>

请注意，还有一个 Text Field，它是一个单行文本组件。你正在寻找 Text View，它可以包含多行文本。

将 text view 和 button 拖到 canvas 上后，应该看起来像这样：

<div align="center"><img alt="Storyboard 中的 About 屏幕" src="http://imgur.com/tZUWemz.png"/></div><center>Storyboard 中的 About 屏幕</center>

<br>

➤ 双击 text view 以使其内容可编辑。默认情况下，text view 包含一大堆假拉丁语占位符文本（也称为 “Lorem Ipsum”）。

将此新文本复制粘贴到其中：

```
*** Bull’s Eye ***

Welcome to the awesome game of Bull’s Eye where you can win points and fame by dragging a slider.

Your goal is to place the slider as close as possible to the target value. The closer you are, the more points you score. Enjoy!
```

你也可以将该文本粘贴到 text view 的 Attributes inspector 中，如果你觉得那样更简单的话。

➤ 确保取消选中 **Editable**（可编辑）设置，否则用户实际键入内容到 text view。对于这个游戏，它应该设置为只读。

<div align="center"><img alt="The text view 的 Attributes inspector" src="http://imgur.com/UERdaF5.png"/></div><center>The text view 的 Attributes inspector</center>

<br>

屏幕设计就到此为止，告一段落先。

➤ 单击 **View Controller** 中的 **(i)** button将其选中。然后按住 Ctrl 并拖动到 **About** 屏幕。

<div align="center"><img alt="按住 Ctrl 从一个 view controller 拖动到另一个 view controller 以创建 segue" src="http://imgur.com/CPwILyR.png"/></div><center>按住 Ctrl 从一个 view controller 拖动到另一个 view controller 以创建 segue</center>

<br>

➤ 放开鼠标按钮，弹出窗口中会显示多个选项。选择 **Present Modally**。

<div align="center"><img alt="选择要创建的 segue 类型" src="http://imgur.com/FJ6waoe.png"/></div><center>选择要创建的 segue 类型</center>

<br>

现在，两个屏幕之间将出现一个箭头。此箭头表示 segue。

➤ 单击箭头以将其选中。Segues 也有属性。在 **Attributes inspector** 中，选择 **Transition**（过渡），**Flip Horizontal**（水平翻转）。这是 UIKit 用来在这些屏幕之间移动的动画。

<div align="center"><img alt="改变 segue 的 attributes" src="http://imgur.com/fmgp7XY.png"/></div><center>改变 segue 的 attributes</center>

<br>

➤现在可以运行应用程序。按 **(i)** button查看新屏幕。

<div align="center"><img alt="The About 屏幕将显示一个翻转动画" src="http://imgur.com/wwtPpba.png"/></div><center>The About 屏幕将显示一个翻转动画</center>

<br>

The About 屏幕应该显示一个整洁的动画。很好，这似乎运转正常。

然而，这里有一个明显的缺点：点击 Close button 似乎没有效果。一旦用户进入 About 屏幕，她就永远也离不开了... 那听起来不像是友好的用户界面设计。

Segues 的问题是，只有一种方式。要关闭此屏幕，你必须将一些代码连接到 Close button。作为一个崭露头角的 iOS 开发者，你已经知道如何做：使用 action method！

这次你将添加 action method 到 AboutViewController 而不是 ViewController，因为 Close button 是 About 屏幕的一部分，而不是主游戏屏幕。

➤ 打开 **AboutViewController.swift** 并将其内容替换为以下内容：

```swift
import UIKit

class AboutViewController: UIViewController {

  @IBAction func close() {
    dismiss(animated: true, completion: nil)
  }
}
```

这个代码在 close() action method 里面告诉 UIKit 用动画关闭 About 屏幕。

如果你说，dismiss(animated: false, ...)，那么将没有页面翻转这个效果，主屏幕会立即重新出现。从用户体验的角度来看，通常最好使用微妙的动画来显示从一个屏幕到另一个屏幕的过渡。

别忘了，你还有一个最后一步，连接 Close button Touch Up Inside 事件到这个新的关 close action。

➤ 打开 storyboard 并按住 Ctr l键从 **Close** button 拖动到 About scene 的 View Controller。嗯，奇怪，关闭动作应该列在这个弹出窗口，但没有。相反，你看到的弹出窗口，和之前你做 segue 时相同：

<div align="center"><img alt="The close action 不会在弹出窗口中列出" src="http://imgur.com/iDWveR6.png"/></div><center>The close action 不会在弹出窗口中列出</center>

<br>

**练习：**奖励积分，如果你能发现错误。这是一个非常常见的，令人沮丧的！——错误。

问题是，storyboard 中的这个 scene 还不知道它自己代表 AboutViewController。

你首先添加了 AboutViewController.swift 源文件，然后将一个新的 view controller 拖到 storyboard 中，但是你没有告诉 storyboard，这个新的 view controller 的设计实际上属于 AboutViewController。（这就是为什么在 outline pane 中只是说 View Controller 而不是 About View Controller。）

➤ 幸运的是，这很容易补救。在 Interface Builder 中，选择 About scene 的 **View Controller**，然后转到 **Indentity inspector**（即 Attributes inspector 左侧的按钮）。

➤ 在 **Custom Class** 下，键入 **AboutViewController**。

<div align="center"><img alt="The About screen 的 Identity inspector" src="http://imgur.com/bctNvv0.png"/></div><center>The About screen 的 Identity inspector</center>

<br>

输入前几个字符后，Xcode 会自动完成此操作。如果没有，请仔细检查是否确实选择了 View Controller，而不是其中的一个 view。（The view controller 也应该有一个蓝色边框，表示它被选中）

现在你应该能够将 Close button 连接到 action method。

➤ 在 outline pane 中，从 **Close** button 按住 Ctrl 向左拖动到 **About view Controller**。这应该是老一套了。弹出菜单现在有 close action 的选项（在已发送事件下）。将 button 连接到该 action。

➤ 再次运行应用程序。你现在应该可以从 About 屏幕返回。

恭喜！这完成了游戏。所有的功能完备了——我可以保证——没有 bugs，以破坏乐趣。

但你必须承认游戏仍然看起来不是很好。如果就以当前形式你把它放在 App Store 上，我确定不会有很多人会兴奋的下载它。幸运的是，iOS 让你能够非常容易创建好看的应用程序，所以让我们给 Bull's Eye 一个改造。

你可以在教程的源代码文件夹中的 **06 - About Screen** 下找到应用程序的项目文件。

##使它看起来美观

在 landscape 模式中的应用程序不显示 iPhone 状态栏，除非你告诉他们。这是我们制作的一个很棒的应用程序。游戏需要更身临其境的体验，状态栏应该隐藏起来。

在 iOS 7 及以前版本中，状态栏不会自动消失在 landscape 模式下，本教程的早期版本包括如何从应用程序中删除状态栏的冗长的说明。

即使这不再需要了，仍然有一些事情你可以做，以改善 Bull's Eye 处理状态栏的方式。

首先，你将从 storyboard 中删除状态栏。

➤ 打开 **Main.storyboard** 并选择 **View Controller**。 转到 **Attributes**

**inspector** 并在 **Simulated Metrics** 下将 **Status Bar**（状态栏）设置为 **None**（无）。

这会从 storyboard 中删除状态栏（你应该会看到电池图标从两个 scenes 的右上角消失）。

<div align="center"><img alt="从 view controller 中删除状态栏" src="http://imgur.com/REb6MTo.png"/></div><center>从 view controller 中删除状态栏</center>

<br>

此设置不会影响应用运行时发生的情况。这就是为什么这一部分被标记为 **Simulated Metrics**。Interface Builder 只是假设有一个状态栏作为视觉设计辅助，所以你可以看到你的屏幕设计看起来有一个状态栏在顶部。

尝试启用一些其他 simulated 选项，然后运行应用程序; 你会看到它不会产生影响。

要永久删除状态栏的最后一步是更改应用程序的配置。

➤ 转到 **Project Settings** 屏幕，向下滚动到 **Deployment Info**。 在 **Status Bar Style** 下，选中 **Hide status bar** 选项。

这也将在应用程序启动期间隐藏状态栏。

<div align="center"><img alt="应用程式启动时隐藏状态栏" src="http://imgur.com/QYU14H9.png"/></div><center>应用程式启动时隐藏状态栏</center>

<br>

在应用程序启动时隐藏状态栏是个好主意。操作系统需要几秒钟时间将应用程序加载到内存并启动它，在此期间，状态栏保持可见，除非您使用此选项隐藏它。

这只是一个小细节，但一个平庸的应用程序和一个伟大的应用程序的区别是，伟大的应用程序做的所有的小细节是正确的。

➤ 就是这样。运行应用程序，您会看到状态栏是历史记录。

**Info.plist**

项目设置屏幕中的大多数选项（例如支持的设备方向以及状态栏在启动期间是否可见）都存储在应用程序的 Info.plist 文件中。

Info.plist 是应用程序包内的一个配置文件，它告诉 iOS 应用程序的行为方式。它还描述了应用程序的某些特征，真正适合其他任何地方，如其版本号。

使用以前版本的 Xcode，你经常不得不手动编辑 Info.plist，但是使用 Xcode 8 这就不再需要了。你可以直接从 Project Settings 中进行大部分更改。

但是，了解一下 Info.plist 存在以及它是什么样子是没有坏处得。

➤ 转到 **Project navigator** 并选择名为 Info.plist 的文件以查看其内容。

<div align="center"><img alt="" src="http://imgur.com/fZ8ABUB.png"/></div>

<br>

The Info.plist 文件只是配置选项及其值的列表。大多数这些可能对你没有意义，但是没关系——他们也不总是对我有意义。

请注意，选项 **Status bar is initially hidden**（状态栏最初是隐藏的）。它的值为 YES。这是你刚才更改的选项。

###调整图形

摆脱状态栏只是第一步。我们想从这里：

<div align="center"><img alt="打哈欠..." src="http://imgur.com/P1WNQay.png"/></div><center>打哈欠...</center>

<br>

得到到更像这样的东西：

<div align="center"><img alt="Cool :-)" src="http://imgur.com/0DK4egq.png"/></div><center>Cool :-)</center>

<br>

实际 controls 不改变。你只需使用图像来调整外观，并且还可以调整 color 和字体。

你可以在 background，button，甚至 slider 上放置图像，以自定义其外观。图片应为 PNG 格式。

如果你是画图白痴，那么不用担心，我已经为你提供了一套图像。但如果你有疯狂的 Photoshop 技术，那么一切手段继续前进，设计自己的图标。

本教程自带的 Resources 文件夹包含一个名为 Images 的子文件夹。你将首先将这些图像导入 Xcode 项目。

➤ 在 **Project navigator**，找到 **Assets.xcassets** 并单击它。

这是应用程序所谓的 asset 目录，它包含应用程序所有的图像。现在，它是空的。其唯一的内容是应用程序图标的占位符，拟很快就会添加。

<div align="center"><img alt="The asset 目录最初为空的" src="http://imgur.com/VW1yic5.png"/></div><center>The asset 目录最初为空的</center>

<br>

➤ 在窗格底部有一个 + 按钮。单击它，然后选择 **Import...**（导入）选项。

<div align="center"><img alt="选择 Import 将现有图像放入 asset 目录" src="http://imgur.com/hImLVun.png"/></div><center>选择 Import 将现有图像放入 asset 目录</center>

<br>

Xcode 显示文件选择器。从本教程的资源中选择 Images 文件夹，然后按 ⌘ + A 选择此文件夹中的所有文件。

<div align="center"><img alt="选择要导入的图像" src="http://imgur.com/t9N4Cxe.png"/></div><center>选择要导入的图像</center>

<br>

单击 **Open**，Xcode 将该文件夹中的所有图像文件复制到 asset 目录中：

<div align="center"><img alt="图像现在位于 asset 目录中" src="http://imgur.com/j7cR7ea.png"/></div><center>图像现在位于 asset 目录中</center>

<br>

如果 Xcode 添加了一个名为 “Images” 的文件夹，而不是单个图像文件，则再次尝试，这时请确保在单击打开之前选择 Images 文件夹中的文件而不是文件夹本身。

**1x, 2x 和 3x 显示**

目前，asset 目录中设置的每个图像只有一个用于 “2x” 图像的插槽，但你也可以指定 1x 和 3x 图像。拥有不同大小的同一图像的多个版本，可让你的应用程序支持现有的各种 iPhone 和 iPad 显示器。

**1x** 是用于低分辨率屏幕，具有大的，块状像素的。实际上没有低分辨率的设备，可以运行 iOS 10——他们太老了，所以你不可能再遇到许多 1x 图像了。1x 只是一个问题，仅当你仍然需要设计一个支持 iOS 9 或甚至 iOS 8 的应用程序。

**2x** 是用于高分辨率视网膜屏幕。这涵盖了大多数现代 iPhone，iPod touch 和 iPad。视网膜图像是低分辨率图像的两倍，因此是 2x。你刚刚导入的图片为 2x 图片。

**3x** 是为超高分辨率的 Retina 高清屏幕的 iPhone 6s Plus 和 7 Plus 设计的。如果你希望你的应用程序在这些顶级的 iPhone 模型上有超清晰的图像，那么你可以将它们放入 asset 目录中的 “3x” 插槽。

图像文件有一个特殊的命名约定。如果文件名以 @2x 或 @3x 结尾，那么它被认为是 Retina 或 Retina HD 版本。低分辨率 1x 图像没有特殊名称（你不必写 @1x）。

##放置壁纸

让我们开始将白色 background 变成一些更奇特。

➤ 打开 **Main.storyboard**。进入对 **Object Library** 并找到一个 Image View。（提示：如果你在 Object Library 底部的搜索框中键入 “image”，则会快速过滤掉所有其他 views）。

<div align="center"><img alt="The Object Library 中的 Image View control" src="http://imgur.com/REisqla.png"/></div><center>The Object Library 中的 Image View control</center>

<br>

➤ 拖动在现有用户界面的顶部的 image view。只要它在 Bull’s Eye View Controller 内部，你把它放在哪里并不重要。

<div align="center"><img alt="拖动 Image View 到 view controller" src="http://imgur.com/2neuqvF.png"/></div><center>拖动 Image View 到 view controller</center>

<br>

➤ 在仍选择 image view 的情况下，转到 **Size inspector**（大小检查器）（即 Attributes inspector 旁边的那个），并将 X 和 Y 设置为 0，将 Width（宽度）设置为 568，将 Height（高度）设置为 320。

这将使 image view 覆盖整个屏幕。

<div align="center"><img alt="The Image View的 Size inspector 设置" src="http://imgur.com/LJV1iC6.png"/></div><center>The Image View的 Size inspector 设置</center>

<br>

➤ 转到 image view 的 **Attributes inspector**。在顶部有一个名为 Image 的选项。单击向下箭头，然后从列表中选择 **Background**。
这将把来自 asset 目录的 “Background” 组的图像放入 image view。

<div align="center"><img alt="在 Image View 上设置 background 图像" src="http://imgur.com/eLAITVS.png"/></div><center>在 Image View 上设置 background 图像</center>

<br>

现在只有一个问题：图像现在盖住了所有其他的 controls。有一个简单的解决办法; 你必须将 image view 移动到其他 views 的后面。

➤ 在 Xcode 菜单栏中屏幕顶部的 **Editor** 菜单中，选择 **Arrange**（排列）**→ Send to Back**（发回）。

有时 Xcode 给刁难你（它仍然有几个 bugs）。如果是，请尝试取消选择 Image View，然后再次选择它。 现在 Send to Back 菜单项应该可用。（译者注：因为有时候它是灰色的不可选中）

或者，在 outline pane 中拾取 image view，并将其拖动到顶部，恰好在 View 下方，以完成相同的操作。

你的界面现在应该如下所示：

<div align="center"><img alt="游戏有了新的 background 图像" src="http://imgur.com/FioXpDV.png"/></div><center>游戏有了新的 background 图像</center>

<br>

➤ 对 **About View Controller**。添加一个 Image View 并给它相同的 “Background” 图像。

在 background 上苦下一番功夫后。运行应用程序，惊讶一下吧！

##更改 labels

因为 background 图像非常暗，黑色 labels 变得难以阅读。幸运的是，Interface Builder 可以改变它们的 color，当你使用它时，你也可以改变字体。

➤ 仍然在 storyboard 中，选择顶部的 label，打开 **Attributes inspector** 并单击 **Color** 项目。

<div align="center"><img alt="设置 label 上的文字的 color" src="http://imgur.com/yLxRXXq.png"/></div><center>设置 label 上的文字的 color</center>

<br>

这将打开 Color Picker（颜色选择器）。它有几种选择 color 的方法。我喜欢 sliders（第二个选项卡）。如果您看到的是灰度 slider，请从顶部的选择框中选择 RGB Sliders。（译者注：哈哈，又是我们的老朋友 Slider，可见他在 UI 中多么常见）

➤ 选择 pure white color（纯白色），Red（红色）：255，Green（绿色）：255，Blue（蓝色）：255，Opacity（不透明度）：100％。

➤ 从 Attributes inspector 中单击 Shadow（阴影）项。这允许你向 label 添加微妙的 shadow。默认情况下，此 color 是透明的（也称为 “Clear Color”），因此你不会看到 shadow。使用 Color Picker，选择 pure black color that is half transparent（半透明的纯黑色），Red：0，Green：0，Blue：0，Opacity：50％。

注意：有时当你更改 Color 或 Shadow 属性时，view 的 background color 也会更改。这是 Xcode 中的一个 bug。当这种情况发生时，把它重置为 Clear Color。

➤ 将 **Shadow Offset**（阴影偏移）更改为 Horizontal（水平）：0，Vertical（垂直）：1。这将 shadow 置于 label 下方。

你选择 shadow 是非常微妙的。如果你不确定它实际上是否可见，请将 vertical offset（垂直偏移）在 1 和 0 之间切换几次。仔细观察，你应该能看到差别。正如我所说，这是非常微妙。

➤ 单击 Font（字体）属性的 [T] 图标。这将打开 Font Picker（字体选择器）。

默认情况下，选择系统字体。这使用用户设备的标准字体，在 iOS 10 是 San Francisco。这是一个很好的字体，但我们想要一些能使这个游戏更刺激的。

<div align="center"><img alt="带有 System font 的 Font picker（带有系统字体的字体选择器）" src="http://imgur.com/1APBlzq.png"/></div><center>带有 System font 的 Font picker（带有系统字体的字体选择器）</center>

<br>

➤ 选择 **Font: Custom**。这启用了 Family 区域。选择 **Family: Arial Rounded MT Bold**。将 size 设置为16。

<div align="center"><img alt="设置 label 的 font" src="http://imgur.com/89DXzr0.png"/></div><center>设置 label 的 font</center>

<br>

➤ The label 还具有属性 **Autoshrink**（自动缩放）。确保将其设置为 **Fixed Font Size**（固定字体大小）。

如果启用，Autoshrink 将动态更改 font 的 size，如果文本大于 label。这在某些应用程序是有用的，但不是在这一个。相反，你将更改 label 的 size 以适应文本，而不是其他方式。（译者注：就是你输入很多字的话会拉长标签控件，使之变形，不再美观）

➤ 选择 label 后，在键盘上按 ⌘=，或从 **Editor** 菜单中选择 Size to Fit Content（适应内容大小）。

（如果 Size to Fit Content 菜单项是被禁用状态（灰色不可选择），则取消选择 label 并再次选择它。有时 Xcode 会对选择的是什么东西感到困惑。这破工具）

The label 现在将变得略大或略小，以便它紧贴文本。如果在更改 font 时文本被截断，现在它将再次完全显示。

你不必逐一设置其他 label 的这些属性；这将是一个庞大的工程。你可以通过选择多个 label，然后将这些更改应用于全部选择来快速搞定这件事。

➤ 单击 **Score:** label 以将其选中。按住 ⌘，然后点击 **Round:** label。 现在两个 labels 都将被选中。 重复上面对这些 labels 的操作：

- 将 Color 设置为 pure white，100％ opaque。
- 将 Shadow 设置为 pure black，50％ opaque。
- 将 Shadow Offset 设置为 0 horizontal，1 vertical。
- 将 Font 设置为 Arial Rounded MT Bold，size 为 16。
- 确保 Autoshrink 设置为 Fixed Font Size。

如你所见，在我的 storyboard 中，文本不再适合于 Score 和 Round labels：

<div align="center"><img alt="文字太大，无法适合 Score 和 Round labels 中的所有文本 labels" src="http://imgur.com/q3moWjH.png"/></div><center>文字太大，无法适合 Score 和 Round labels 中的所有文本 labels</center>

<br>

你可以通过拖动边框来增大 labels 的大小，也可以手动调整大小，也可以使用 **Size to Fit Content** 选项（⌘=）。 我喜欢后者，因为它工作量更少。

提示：Xcode 足够聪明，记住你最近使用的 Color。而不总是进入 Color Picker，你可以简单地从 Recently Used Colors（最近使用的颜色）菜单中选择其中一种。

点击小箭头，弹出菜单：

<div align="center"><img alt="快速访问最近使用的 colors 和几个方便的预设¨ labels" src="http://imgur.com/bdlckmC.png"/></div><center>快速访问最近使用的 colors 和几个方便的预设</center>

<br>

**练习：**你还下几个 labels。重复你刚才做的为其他 labels。它们应该都变成白色，具有相同的 shadow 和具有相同的 font。但是，slider（1 和 100）两侧的两个 labels 的 font size 为 14，而其他 labels（目标值，分数和回合数的 labels）的 font size 设置为 20，让它们变得显眼。

因为你改变了一些 labels 的尺寸，你仔细构造布局可能已经变得有些乱了。你可能想要清理一下。

在这一点上，我的屏幕看起来像这样：

<div align="center"><img alt="设计 labels 后，storyboard 看起来像什么" src="http://imgur.com/ccUWb9A.png"/></div><center>设计 labels 后，storyboard 看起来像什么</center>

<br>

好吧，它现在开始看起来有那么点像模像样了。顺便说一下，随时都可以尝试更改 fonts 和 colors。如果你想让它看起来完全不同，那么久去做吧。这是你的应用程序！

##The buttons

改变 button 的外观工作方式与上面的步骤非常相似。

➤ 选择 **Hit Me** button。在 **Size inspector** 中将 Width 设置为 100，Height 设置为 37。

➤ 将 button 的位置居中在 background image 的内圆上。

➤ 转到 **Attributes inspector**。将 **Type** 从 System 更改为 **Custom**（自定义））。

一个 “system” button 只有一个 abels，没有边框。通过使它成为一个自定义 button，你用可以用任何方式，变吃成你想要的样式。

➤ 按 **Background** 字段上的箭头，然后从列表中选择 **Button-Normal**。

➤ 将 **Font** 设置为 **Arial Rounded MT Bold**，size 为 20。

➤ 将 **Text Color**（文本颜色）设置为 Red：96，Green：30，Blue：0，Opacity：100％。这是一个暗棕褐色。

➤ 将 **Shadow Color** 设置为 pure white，50％ opacity。The shadow offset 应为 Width 0，Height 1（由于某种原因，它们在此处不称为 horizontal 和 vertical）。

<code class="highlighter-rouge"><strong>混合</strong></code>

`将 opacity 设置为小于 100％ 的任何值将使颜色稍微透明（不透明度为 0％ 的透明度）。部分透明度使 color 与 background 混合，使其看起来更柔和。`

`尝试将 shadow color 设置为 100％ opaque pure white，然后观察区别。`

这将在 “default”（默认）状态下完成 Hit Me button 的设置：

<div align="center"><img alt="在 default 状态下 Hit Me button 的 attributes" src="http://imgur.com/zdYjS8N.png"/></div><center>在 default 状态下 Hit Me button 的 attributes</center>

<br>

Buttons 可以有多个状态。当你点击一个 button 并按住它，它应该显示 “pressed down”（按下），让你知道，当你举起你的手指，该 button 将被激活。这被称为 *highlighted* 状态，并且是用户的重要的视觉线索。

➤ 在保持选择 button 的情况下，单 **State Config**（状态配置）设置，然后从菜单中选择 **Highlighted**。现在，此部分中的 attributes 反映 button 的 highlighted 状态。

➤ 在 **Background** 字段中，选择 **Button-Highlighted**。

➤ 确保 highlighted 的 **Text Color** 与以前的 color 相同（Red 96，Green 30，Blue 0 或从 Recently Used Colors 菜单中选择）。再次将 **Shadow Color** 更改为 half-transparent white（半透明白色）。

➤ 检查 **Reverses On Highlight**（高亮反转）选项。这将使得当用户轻触 button 时 label 的外观看起来像是被按下。

你也可以改变其他属性，但不要太过分了。The highlighted 效果不应该太耀眼。

<div align="center"><img alt="The attributes for the highlighted Hit Me button" src="http://imgur.com/JS3gz9E.png"/></div><center>The attributes for the highlighted Hit Me button</center>

<br>

要在 Interface Builder 中测试 button 的 highlighted 外观，你可以切换 **Control** 部分中的 **Highlighted** 显示框，但是测试完记得切换回去，否则当显示屏幕时 button 看起来就像是被按下去一样。

这是为了 Hit Me button。对 Start OVer button 进行样式设置非常相似，只是将其标题文本替换为图标。

➤选择 **Start Over** button 并更改以下属性：

- 将 Type 设置为 Custom。
- 从 button 中删除文本 “Start Over”。
- 对于 Image，选择 **StartOverIcon**。
- 对于 Background，选择 **SmallButton**。
- 将 Width和 Height 设置为 32。

你不会在此 button 上设置 highlighted 状态，不过要让 UIKit 处理这个。如果你没有为 highlighted 的状态指定不同的图像，UIKit 将自动使 button 变暗以指示它已哦按下。

➤ 对 **(i)** button 进行相同的更改，但此次为 Image 选择 **InfoButton**。

用户界面几乎完成。只剩下 slider 还没有完成...

<div align="center"><img alt="即将完成" src="http://imgur.com/FsYqo4T.png"/></div><center>即将完成</center>

<br>

##The slider

不幸的是，你只能在 Interface Builder 中自定义滑块的一小部分属性。对于这个游戏需要的更高级的定制——把你自己的图像放在 slider 和轨道上——你必须靠编写源代码来实现。
你在 Interface Builder 中完成的所有操作都可以在代码中完成。例如，设置 button 上的颜色可以通过向 button 发送 setTitleColor() 消息来完成。

但是，我发现在可视化编辑器（如Interface Builder）中设计要比编写等效的源代码容易得多。但对于 slider 你没有办法，因为官方没有在可视化编辑器中为 slider 提供很多可以自定义的属性。

➤ 转到 **ViewController.swift**，并将以下内容添加到 viewDidLoad()：

```swift
let thumbImageNormal = UIImage(named: "SliderThumb-Normal")!
slider.setThumbImage(thumbImageNormal, for: .normal)

let thumbImageHighlighted = UIImage(named: "SliderThumb-Highlighted")!
slider.setThumbImage(thumbImageHighlighted, for: .highlighted)

let insets = UIEdgeInsets(top: 0, left: 14, bottom: 0, right: 14)

let trackLeftImage = UIImage(named: "SliderTrackLeft")!

let trackLeftResizable =
                 trackLeftImage.resizableImage(withCapInsets: insets)
slider.setMinimumTrackImage(trackLeftResizable, for: .normal)

let trackRightImage = UIImage(named: "SliderTrackRight")!
let trackRightResizable =
                 trackRightImage.resizableImage(withCapInsets: insets)
slider.setMaximumTrackImage(trackRightResizable, for: .normal)
```