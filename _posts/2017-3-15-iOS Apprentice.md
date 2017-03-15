---
layout: post
title: "iOS Apprentice 1 Getting Started v5.0 （译）"
date:   2017-03-15
excerpt: "译至 40 页"
tags: [program, iOS, translate]
comments: true
---

`Tips：专有名词我只会在它第一次出现时翻译，后续不再翻译。`

- `毕竟你要和全英文的编译器打交道，译后你甚至可能找不到它在编译器的何处。`

- `当你以后进入公司，保留着这种习惯一定会影响你与同事的交流。`

- `上网翻阅资料或询问他人时，无论哪里对于专有名词都是直接引用。`

  ---

<br>

<h1 align="center">iOS Apprentice 第一章</h1>

<center><strong>Aurevoir Xavier 译</strong></center>

<br>

嗨！我是 Matthijs Hollemans，一名全职iOS开发人员和 [www.raywenderlich.com](www.raywenderlich.com) 的辅导团队成员。

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

我们的第一个工作是下载并安装 Xcode 和 iOS SDK（软件开发工具包）。

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
} }
```

<center>上面的代码片段取自于一个声音合成器程序中</center>

<br>

它几乎看起来就像是某些有意义的东西。即使你以前从来没有编过程，你可以通过排序，弄清楚其中发生了什么。这几乎就是英语。（译者注：好好学习英语吧，也许我翻译本书是个错误）

Swift 是一门新兴的同时又非常热门的语言，它将传统的 object-oriented（面向对象）编程与函数式编程的各方面相结合。幸运的是，Swift 有许多与其他流行编程语言相同的东西，所以如果你已经熟悉 C#，Python，Ruby 或 Javascript，你会在使用 Swift 过程中体会到宾至如归的感觉。

Swift 并不是制作应用程序的唯一选择。直到最近，iPhone 和 iPad 应用程序都是使用 Object-C 编写的（译者注：乔老大留下宝贵财富，还是很有分量的），Object-C 是一门由 C 语言在 object-oriented 这一方面拓展而来的。由于是那个时代 C 语言的产物，Object-C 难免有着一些粗糙的棱角，并不真正符合现代开发商的需求。这就是为什么苹果创造了一种新的语言。

Object-C 仍然会存在一段时间，但显然，iOS 开发的未来是属于 Swift。所有 cool 孩子都已经在使用它了。

C++ 是另一种由 C 衍生出来的 object-oriented 编程语言。它非常强大，但作为一个刚入门的程序员，你可能会想要远离他。我只提一下它，因为 C++ 也可以用于编写 iOS 应用程序，并有着一段不羁之恋，C++ 与 Object-C 称之为 Object-C++，你可能会不时遇到。

我可以在 iOS Apprentice 的一开始深入讨论 Swift 的功能，但那样你可能会睡着。所以，我们来慢慢的解释语言，非常简单，等你适应了，再做更深入的讲解。

在一开始，一般概念——什么是变量，object（对象），如何调用方法等——远比详细信息重要。虽然缓慢但毫无疑问，我会将 Swift 语言所有的秘密都揭露给你。

你准备好开始编写你生涯中的第一个 iOS 应用程序了吗？

## Bull's Eye 游戏

在第一课中，你将创建一个名为 Bull‘s Eye 的游戏。这是最终效果：

<div align="center"><img alt="完成的 Bull's Eye" src="http://imgur.com/YoEGCsp.png"/></div><center>完成的 Bull's Eye</center>

<br>

目标是滑动图中这个看起来像牛眼一样的 Slider（滑块）（范围 1 ～ 100），使其尽可能的贴近系统给出的随机值。在上面的截图中，目标是将 “牛眼” 滑动到 22 的地方，因为看不到滑块的当前值，所以全靠目测了。

当你对你的估计有信心时，按下 “Hit Me!” button，弹出的窗口（也称为 alert（提醒））会告诉你，你获得了多少分：

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

你可能有一个很酷的想法，但当你坐下来写程序时，整个事情似乎要把你压垮。有这么多事要做……从哪里开始？通过将工作量分为一个一个小的部分，你就可以使项目看起来没有那么令人生畏——你总是可以找到一个简单而小巧的步骤，以便创建一个良好的开端，并从那里开始。

这没什么大不了的，如果这个练习让你觉得困难。只是因为你是个刚开始学习这方面知识的新人而已！随着你对软件工作原理理解的加深，将能够更从容的将工作量合理分配并管理。

这是我的想法。我只是根据游戏的描述，并把它分割成一块一块：

- 在屏幕上放置一个 button（按钮），并将其标记为 “Hit Me!”。
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

确保未选中底部的三个选项—— Use Core Data（使用 Core 数据），Include Unit Tests（包括单元测试）和 Include UI Tests（包括UI测试）。你将不会在这个项目中使用这些。

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

➤ **Run** 按钮旁边是 **Stop**(停止) 按钮（方形）。 按此退出应用程序。

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

目前，storyboard 只包含一个屏幕或场景，由 Interface Builder Canvas（画布）中间的一个矩形表示。

<code class="highlighter-rouge"><strong>注意：</strong>如果你没有看到标记为 “View Controller”（视图控制器） 的矩形，眼前只有一个空白的 Canvas，则使用鼠标或触控板滚动 storyboard。相信我，它一定在某处！还要确保你的 Xcode 窗口足够大。因为 Interface Builder 占用了很多空间...</code>

该 scene（场景）目前有一部 iPhone 6s 或 iPhone 7 的大小。为了保持清爽简洁，你会首先为 iPhone SE 设计一个稍小的屏幕的应用程序。稍后你将会让这款应用程序也是配更大的 iPhone 6s，7 和 Plus。

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

这应该会给你一些有关 UI controls 的想法，因为 iOS 支持使用它们。请注意，Interface Builder 会帮助您布局 controls，通过将 controls 对齐到 view 的边缘和其他 object。这是一个非常方便的工具！

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

<br>

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
from a nib. }
  override func didReceiveMemoryWarning() {
    super.didReceiveMemoryWarning()
    // Dispose of any resources that can be recreated.
}
  @IBAction func showAlert() {
} }
```

初尝 Swift 的感觉如何？合你口味吗？ 在我可以告诉你这是什么意思之前，我首先要介绍一个有关 view controller 的概念。

<br>

<code class="highlighter-rouge"><strong>Xcode 会自动保存</strong></code>

<code class="highlighter-rouge">你不必保存文件，在你对它们进行更改后，因为当你按下 Run 按钮后 Xcode 将自动保存任何修改的文件。然而，Xcode 不是最稳定的软件，有时候它可能会在保存你的更改之前崩溃，所以我仍然想按 <strong>⌘ + S</strong> 定期保存我的文件。</code>

## View controllers

你已经编辑 **Main.storyboard** 文件来构建应用程序的用户界面。它只是一个白色背景上的 button，但它确实是一个实实在在的用户界面。你还向 **ViewController.swift** 添加了源代码。

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

你刚刚所添加到 ViewController.swift 的源代码的作用是让 Interface Builder 知道 controller 有一个名字为 “showAlert” 的操作，它可能会显示一个 alter 弹出窗口。你现在将要做的就是将 button 连接到该操作。

➤ 单击 **Main.storyboard** 返回到 Interface Builder。

左边应该有一个 pane，即 **Outline pane**，其中列出了所有项目你的 stpryboard。如果没有看到该 pane，请单击 Interface Builder canvas 左下角的小切换按钮以显示它。

<div align="center"><img alt="用来显示 Outline pane 的按钮" src="http://imgur.com/uThAxbE.png"/></div><center>用来显示 Outline pane 的按钮</center>

<br>

➤ 单击 **Hit Me** button 将其选中。

选中 “Hit Me” button 后，按住 Ctrl 键，单击 button 并向上拖动到 Outline pane 中的 View Controller 项。你应该会看到 button 和 View Controller 之间出现一条蓝线。

（如果你不想按住 Ctrl，你也可以右键单击和拖动，但在开始拖动之前，请不要放开鼠标按键。）

<div align="center"><img alt="从 button 开始按住 ctrl 并拖动到 View Controller" src="http://imgur.com/GXEDkR6.png"/></div><center>从 button 开始按住 ctrl 并拖动到 View Controller</center>

<br>

一旦你在 View Controller 上，放开鼠标按键，会出现一个小菜单。 它包含两个部分，  “Action Segue”（操作 Segue）和 “Sent Events”（发送事件”），每个下面有一个或多个选项。 你对 Sent Events 下的 **showAlert** 选项感兴趣。这是你先前在 ViewController.swift 的源代码中添加的操作的名称。

<div align="center"><img alt="带有 showAlert 操作的弹出菜单" src="http://imgur.com/tbiY4J1.png"/></div><center>带有 showAlert 操作的弹出菜单</center>

<br>

➤单击 show alert 以选择它。这表明 Interface Builder 在 button 和 @IBAction func show Alert() 之间进行关联。

从现在开始，每当 button 被点击时，将执行 showAlert 操作。这就是如何使 button 和其他controls 互动：你在 view controller 的 Swift 文件中定义一个动作，然后在Interface Builder中进行连接。

你可以看到连接关系，通过 Xcode 窗口右侧的实用程序窗格中的 **Connections inspector**（连接检查器）。

➤ 单击 pane 顶部的小箭头形按钮以切换到 Connections inspector：

<div align="center"><img alt="inspector 显示从 button 到任何其他 object 的连接" src="http://imgur.com/8qKlFD2.png"/></div><center>inspector 显示从 button 到任何其他 object 的连接</center>

<br>

在 Sent Events 部分中，“Touch Up Inside”（触摸内部）事件现在已连接到 showAlert 操作。你同样可以在 Swift 文件中查看连接。

➤ 选择 ViewController.swift 以编辑它。

注意在行 @IBAction func showAlert() 的左边，有一个实心圆？ 点击该圆以显示此操作（译者注：一般这种操作称之为，函数或者方法。原文为：action）所连接的内容。

<div align="center"><img alt="实心圆表示动作连接到某物" src="http://imgur.com/079R0Yo.png"/></div><center>实心圆表示动作连接到某物</center>

<br>

## Button 上的行为

你现在有一个带有 button 的屏幕。该 button 被关联到名为 showAlert 的操作上，当用户点击该 button 时将执行该操作。

然而，目前而言，操作是空的，什么也不会发生（不信试试）。你需要向应用程序提供更多说明。

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

<center>新加入的这几行提供了此操作的实际功能。</center>

<br>

{} 括号之间的命令告诉 iPhone 做什么，它们从上到下依次执行。

showAlert 中的代码创建一个标题为 “Hello，World” 的 alert，它包含一条 “This is my first app!” 消息和一个 label 为 “Awesome” 的 button。

如果你不确定标题和消息之间的区别：都显示文本，但标题稍大，而且采用粗体。

➤ 单击 Xcode 工具栏上的 Run 按钮。如果你没有任何的拼写错误，你的应用程序应该会在模拟器中启动，当你点击 button，应该会看到 alert。

<div align="center"><img alt="alert 弹出动作" src="http://imgur.com/suZqPl0.png"/></div><center>alert 弹出动作</center>

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

应用程序本质上由可以向彼此发送消息的 **objects** 组成。你的应用程序中的许多 objects 由iOS提供，例如 button（UIButton对象）和 alert 弹出窗口（UIAlertController对象）。对于一些 object，你必须自己编程，如 view controller。

这些 object 通过将消息传递给彼此进行通信。当用户点击应用程序中的 “Hit Me” button 时，例如，该 UIButton object 发送消息到你的 view controller。view controller 可以通知更多的 objects。

在 iOS 上，应用程序是事件驱动，这意味着这些 objrcts 侦听某些事件并进行处理。

听起来很奇怪，一个应用程序花大部分时间做...什么没有。它只是坐在那里等待某事件发生。当用户点击屏幕时，应用程序弹出几毫秒的动作，然后它再次回到睡眠，直到迎来下一个事件。

在此方案中你所做的部分就是，由你编写的源代码将在对象接收到此类事件的消息时执行。

在应用程序中，button 的 Touch Up Inside 事件连接到 view controller 的 showAlert 操作。 所以当 button 识别它已被轻敲时，它发送 showAlert 消息到你的 view controller。

在 showAlert 内部，view controller 发送另一个消息，addAction 到 UIAlertController 的 object。为了显示警报，view controller 发送当前消息。

你的整个应用程序将由以这种方式来通信的对象所组成。

<div align="center"><img alt="应用中事件的一般流程" src="http://imgur.com/peQXMv5.png"/></div><center>应用中事件的一般流程</center>

<br>

也许你已经在你的网站上使用过 PHP 或 Ruby 脚本。这个基于事件的模型与 PHP 脚本的工作原理不同。PHP 脚本将从上到下运行，一个接一个地执行语句，直到它到达终点，然后退出。

应用程序，另一方面，不退出，直到用户终止它们（或它们崩溃！）。它们花费大部分时间等待输入事件，然后处理这些事件并回到睡眠状态。

来自用户的输入，大多数是触摸和敲击的形式，是你的应用程序中的最重要的事件源，但也有其他类型的事件。例如，当用户接收到来电时，当它必须重新绘制屏幕时，当定时器倒计时……操作系统就会通知你的应用程序。

你的应用程序执行的所有操作都是由某个事件触发而来的的。

## 按照待办事项列表工作

现在你已经完成了第一个任务，在屏幕上放置一个 button，并使其显示一个 alert，你只需下去列表，勾选其他项目。

你不必真的要以某种特定的顺序去做，虽然一些事情在别的事情之前做有意义。 例如，如果你还没有 slider，则无法读取 slider 的位置。

所以，让我们添加其余的 controls——slider 和 text labels，并将这个应用程序变成一个真正的游戏！

当你完成后，应用程序将如下所示：

<div align="center"><img alt="配有标准 UIKit（界面工具包）controls 的游戏屏幕" src="http://imgur.com/WfRn9F7.png"/></div><center>配有标准 UIKit（界面工具包）controls 的游戏屏幕</center>

<br>

嘿，等一下......这看起来并不像我答应你的那样，展示给你看的游戏那般漂亮！区别在于这都是些标准的 UIKit controls。他们看起来像是直接开箱的样子。

你可能已经看过这个面板，因为它非常适合常规的应用程序。但是因为默认的死沉沉的样子对于一个游戏来说有点枯燥无聊，所以你会在后续课程给它加一些调味料。

<code class="highlighter-rouge"><strong>UIKit 和其他 frameworks（框架）</strong></code>

`iOS 提供了许多 frameworks 或 “kits” 形式的构建块。UIKit frameworks 提供了用户界面的 controls，如 buttons，labels 和 navigation bar。它管理 view controller，通常负责处理应用程序的用户界面。（ UI 代表：用户界面。）`

`如果你不得不得从头开始写所有的东西，你或许要忙上一会儿。相反，你可以在系统提供的 frameworks 之上构建你的应用程序，并利用苹果工程师已经为你做完了的现成的东西。`

`任何你看到的以 UI 开头的 object，例如 UIButton，都来自 UIKit。当你编写 iOS 应用程序时，UIKit framework 将是耗费你大部分时间的地方，但也有些人不会。`

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

我相信你知道一个像素是什么。如果你不知道的话：它是屏幕组成的最小的元素。你的 iPhone 显示的是一个大矩阵的像素，每个像素都可以有自己的颜色，就像一个电视屏幕。 改变这些像素的颜色值在显示器上产生可见图像。像素越多，图像看起来越好越细腻。

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

➤ 在 Interface Builder 中打开 **Main.storyboard**。在 **View as：iPhone SE** 面板中，将 **Orientation** 更改为 lanscape：

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

➤确保选择的是 **General**（常规）选项卡：

<div align="center"><img alt="项目的设置" src="http://imgur.com/UJlJeHf.png"/></div><center>项目的设置</center>

<br>

在 **Deployment Info**（部署信息）部分中，有一个用于 **Device Orientation** 的选项。

➤仅检查 Landscape Left 和 Landscape Right 选项，并保留未选中的 Portrait 和 Upside Down（倒置）选项。

再次运行应用程序，它将非常正确的从一开始就以 landscape 方向启动。

## Objects，数据（data）和方法（methods）



是时候来一些编程理论了。是的，你逃不过的。

Swift 是一种所谓的 “object-oriented” 编程语言，这意味着你做的大多数事情的时候都涉及到某种东西。我已经反复提了几次，一个应用程序包含着能彼此发送消息的 object。

编写 iOS 应用程序时，将使用系统为您提供的 object，例如 UIKit 中的 UIButton object，并且你将创建自己的对象，例如 view controller。

那么 object 究竟 *是* 什么呢？想像一个 object 作为你的程序的构建块。（译者注：金字塔上的石块，积木建筑中的积木块）

程序员喜欢将相关的功能分组为 object。这个 object 负责解析文件，那个 object 知道如何在屏幕上绘制图像，而另一个 object 可能会执行困难的计算。

每个 object 负责程序的特定部分。在一个完整的应用程序，你会有许多不同类型的 object（几十或甚至数百）。

即使你的小启动器应用程序也已经包含几个不同的 object。你花了最多的时间，到目前为止的是 ViewController。Hit ME button 也是一个 object，alert 弹出。 和你的 alert text——“Hello, World!” 和 “This is my first app!”——他们都是 object。

该项目还有一个名为 AppDelegate 的 object，即使你将忽略它在此课程（但如果你好奇，可以随意查看它的源文件）。这些 object 无处不在！

一个 object 可以具有数据和功能：

