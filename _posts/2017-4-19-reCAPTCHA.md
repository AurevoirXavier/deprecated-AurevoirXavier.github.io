---
layout: post
title: "I’m not a human: Breaking the Google reCAPTCHA"
date:   2017-04-19
excerpt: "我虽非人类：且看我如何攻破 Google reCAPTCHA 验证机制"
tags: [captcha, google, program, translate]
comments: true
---

---

<center><h1 style="">我虽非人类：且看我如何攻破 Google reCAPTCHA</h1></center>

<center><strong>Aurevoir Xavier 译</strong></center>

<center><h2><i>Suphannee Sivakorn, Jason Polakis, and Angelos D. Keromytis</i></h2></center>

<center><i>[suphannee, polakis, angelos]@cs.columbia.edu Columbia University, New York NY, USA</i></center>

---

自从验证码被创造出来那一天，就广泛地运用于阻止攻击者的不合法操作。尽管验证码能在一定程度上拦截恶意攻击者，但是在经济利益的诱惑下，各种针对验证码的自动化攻击方式如雨后春笋般冒出，那么验证码服务也就相应地做出改进。然而近来，出现了一种针对文本验证码的新型且通用攻击方式。Google 也适时地公布了 reCaptcha 的最新版本。最新版本有两个目标：一是减少合法用户通过验证码认证的成本 (省时省力)，二是提供了对计算机来说，比文本识别更有难度的验证码。reCaptcha 是由一个 “高级的风险分析系统” 驱动的，这种系统通过分析收到的请求，挑出适合难度的验证码返回给用户。用户可能需要勾选一个复选框，或者需要挑出描述相同内容的一组图像。

在这篇论文中，我们对 reCaptcha 和多种多样的用户请求是如何影响风险分析系统做判断，做了系统研究。通过大量的实验，我们发现一些缺陷，攻击者可以通过这些缺陷来轻松地影响风险分析系统，绕过验证码限制，进而实施大规模的攻击。随后，我们利用深度学习技术进行图像的语义注释，设计了一种新颖的低成本攻击方式。我们的攻击系统非常有效，能够自动解决 70.78% 的图像 reCaptcha，每个验证码的认证只平均只耗费 19s。我们对 Facebook 的图像验证码也做了测试攻击，成功率达到了 83.5%。基于我们的实验所得，我们针对这些攻击，提供了一系列的保护和改善措施。总之，我们的研究专注于 reCaptcha，这些发现有非常广的影响。因为对图像所传达的语义信息的逻辑自动化处理越来越多，越来越频繁，所以，验证码也必然要顺应趋势，在更新奇的方向上做更深的探索。

# 1 了解 reCaptcha

Google 提供的 reCaptcha 服务 [1] 是最广泛使用的验证码服务，已被许多流行网站采用，用于防止自动漫游器进行恶意活动。Google 宣布 [2] 部署了一个新的 reCaptcha 机制，旨在使其更加人性化和安全。

**网页控件**

当访问由 reCaptcha 保护的网页时，会显示一个小的网页控件 (如图 1 (a) 所示)。这个控件的 JavaScript 代码被模糊化，为了防止被第三方分析。当它加载时，会收集有关用户浏览器的信息并将其发送回服务器。此外，它会执行一系列检查以核实用户的浏览器。

**工作流程**

一旦用户点击了复选框，就会向 Google 发送一个请求，其中包括 (i) `Referrer`，(ii) 网站的 `sitekey` (在注册 reCaptcha 时获得)，(iii) 提供给 `google.com` 的 cookie，以及 (iv) 由执行此控件的浏览器生成的信息检查 (加密)。然后由先进的风险分析系统分析该请求，最后决定向用户呈现哪种类型的验证码。

<div><div align="center"><img alt="(a) 用户点击复选框之前" src="http://imgur.com/eHshegQ.png"/></div><center>(a) 用户点击复选框之前</center><div align="center"><img alt="(b) 用户点击复选框之后" src="http://imgur.com/OjqRJCz.png"/></div><center>(b) 用户点击复选框之后</center></div><center><strong>图 1. reCaptcha 网页控件</strong></center>

<br>

<div align="center"><img alt="reCaptcha 网页控件" src="http://imgur.com/bejOjrz.png"/></div><center><strong>图 2. reCaptcha 提供的相似图像验证码</strong></center>

**验证码类型**

验证码类型类型因用户而异。如果用户的特定某信用较低，频繁请求或多次回答错误，将会提高验证码的难度。在我们的实验中，我们遇到了以下版本的 reCaptcha：

- ​“无验证码的 reCaptcha” [图 1]。新的用户友好版本，旨在彻底消除解决问题的困难。单击控件的复选框，如果高级风险分析系统认为用户具有很高的信用度，那么验证通过，用户不需要任何操作。对于本文的其余部分，我们将这种类型的验证码统称为复选框验证码。
- 图像 reCaptcha [图 2]。这个新版本是建立在识别具有相似内容的图像的概念上。其包含示例图像和 9 个候选图像，要求用户选择与样本相似的图像。验证码通常会包含描述用户需要选择的图像内容的关键字 (对图像内容的概括性描述)。正确图像的数量一般在 2 和 4 之间。
- 文本reCaptcha [表 1 (a) 至 (e)]。当高级风险分析考虑到用户的信用较低时，将会提供这些扭曲的文字来 (文本验证码)。在用户点击复选框之前，如果用户机器在浏览器的某些检查中失败了，那么分析系统就会返回给用户类似 (e) 这种可靠的验证码，网页控件会自动收取并显示此验证码。在接下来 6 个月的时间里，文字识别码似乎逐渐被淘汰，图像验证码现在是默认的返回类型，因为机器人反而更容易解决这些验证码 [3, 4] 。

<center><strong>表 1. 文本 reCaptcha 的一些例子</strong></center>

|     (a) | ![](http://imgur.com/rDE98fd.png) |     (b) | ![](http://imgur.com/w7oBpZG.png) |
| ------: | :-------------------------------- | ------: | :-------------------------------- |
| **(c)** | ![](http://imgur.com/Q7weiAs.png) | **(d)** | ![](http://imgur.com/YyemWJV.png) |
| **(e)** | ![](http://imgur.com/D3cyxkI.png) |         |                                   |

**解决方案**

一旦验证码对用户展示出来，它必须在 55s 内被回答。否则，用户需要再次单击该复选框以接收新的验证码。一旦用户点击，一个名为 `recaptcha-token` 的 HTML 字段就用会被储存到 token 中。如果用户被判定是合法的，不需要验证码验证，则该 token 在 Google 服务器获取认可。当完成所需的操作时，token 将提交给网站，用于获取认可。网站通过 reCaptcha API 发送验证请求，该 API 包含： (i) 共享密钥，(ii) 响应令牌，以及 (iii)用户的 IP 地址。若收到这个请求的响应，说明认证成功。

# 2 剖析风险分析系统

在本节中，我们将探讨 Google 的高级先进风险分析体系，并确定用户和用户浏览器信息的各种特征值是如何影响其工作的。我们遵循黑盒测试方法来确定系统和测试环境的不同方面是如何影响风险分析过程的。我们的目的是发出由高级风险分析系统认定为合法的验证码，如此一来，我们就能获得最简单的只需按一下就能通过验证的复选框验证码。

## 2.1 浏览历史

Google 的跟踪 cookie 在确定应该向用户呈现何种难度的验证码这一方面方面起着至关重要的作用。我们构建了实验，旨在量化一个特定 cookie 所需的最低浏览历史数量，根据这些 cookie 对合法用户呈现一个复选框验证码。我们探索了多重网络连接设置以及生成浏览历史的活动。例如在我们的分网和美国出口节点的 Tor 网频进行实验。我们自动搜索 Google 的某些关键词，访问搜索出来的链接，观看 Youtube 上的视频，Google 地图上的搜索，访问包含 Google+ 插件和控件的热门网站。令人惊讶的是，我们可以在 cookie 创建后的第 9 天开始时获得一个复选框验证码，而不需要任何浏览活动和网络连接类型，如表 2 所示。我们的实验还显示，每个 cookie 最多可以收到 8 个复选框验证码在一天之内。

<center><strong>表 2. 构造追踪 cookie 和 “模拟” 用户行为</strong></center>

|   Network    | Web Surfing | Account |  Threshold  |
| :----------: | :---------: | :-----: | :---------: |
| Departmental |  Frequent   |   No    |   9th day   |
| Departmental |  Moderate   |   No    |   9th day   |
|     ToR      |  Frequent   |   No    |   9th day   |
|     ToR      |  Moderate   |   No    |   9th day   |
|   **Any**    |  **None**   | **No**  | **9th day** |

## 2.2 浏览器环境

reCaptcha 空间执行一系列的检查是为了检测浏览器的属性或可疑行为。虽然控件的 JavaScript 代码被模糊化以防止分析，但是已经发布了去混淆的代码 (1)。通过返混淆，我们知道了它具体做了什么些检查。在这里，我们将探讨我们的自动浏览器环境的各个方面是如何影响风险分析结果的。

<center><strong>表 3. 我们系统使用的和用户机器包含的不匹配信息的组合</strong></center>

|    Component    | 9-day Cookie |           System runs           |            User-Agent reports            | Captcha  |
| :-------------: | :----------: | :-----------------------------: | :--------------------------------------: | :------: |
|     Browser     |      ✔       |          Firefox/36.0           | {Mobile/8C148 Safari/6533.18.5, Chrome/42.0.2311.135 Safari/537.36} |  image   |
| Browser version |      ✔       |          Firefox/36.0           |    Firefox/{10.0, 35.0, 36.0, 3.0.12}    | checkbox |
| Browser version |      ✘       |          Firefox/36.0           |        Firefox/{10.0, 35.0, 36.0}        |  image   |
| Browser version |      -       |          Firefox/36.0           |              Firefox/1.0.4               | fallback |
| Browser version |      ✘       |           Chrome/42.0           |      Chrome/{15.0.861.0, 4.0.212.1}      |  image   |
| Browser version |      -       |           Chrome/42.0           |             Chrome/3.0.191.3             | fallback |
| Engine version  |      -       | Chrome/42.0; AppleWebKit/537.36 |    AppleWebKit/{528.10, 530.5, 531.3}    | fallback |
| Engine version  |      ✘       | Chrome/42.0; AppleWebKit/537.36 |         AppleWebKit/{532 and up}         |  image   |
| Engine version  |     ✔\|✘     |  Firefox/36.0; Gecko/20100101   |              Gecko/20040914              |  image   |
| Browser/Engine  |      -       | Chrome/42.0; AppleWebKit/537.36 |       Chrome 42/0; Gecko/20100101        | fallback |
| Browser/Engine  |     ✔\|✘     |  Firefox/36.0; Gecko/20100101   |     Firefox/36.0; AppleWebKit/537.36     |  image   |
|    Platform     |      ✔       |          Linux x86_64           | {(Macintosh; Intel Mac OS X 10.8;), (Android; Mobile;), (Windows NT 6.3;)} | checkbox |
|        -        |      -       |                -                |  wrong format or incomplete information  | fallback |
|        -        |      ✔       |   Linux x86_64; Firefox/36.0    | Mozilla/5.0 (iPhone; U; CPU like Mac OS X; en) AppleWebKit/420 (KHTML, like Gecko) Version/3.0 Mobile/1A543a Safari/419.3 | checkbox |

**Canvas 渲染**

Canvas 渲染是一种已知的技术，可以跨机器和浏览器识别用户 [5]。reCaptcha 的 JavaScript 代码创建一个 Canvas 元素并绘制一个预定义的结构。渲染完成后，这个 canvas节点被编码成 base64 格式，并在用户单击复选框时与其他数据一起发回。这些信息可以用于鉴定浏览器的渲染能力，并确定浏览器版本，随后和用户代理登记的信息做比较，查找不同之处。

**用户代理**

为了确定用户代理如何影响用户的信用度，我们按特定的情况给其分组。我们发现，如果用户代理包含过时版本的浏览器或浏览器引擎，则控件会自动将环境视为可疑环境，并为用户提供一个后备验证码 (表1 - (e))。如果浏览器和引擎版本是最新的，但是不符合实验的实际环境 (例如，如果我们使用 Firefox，但报告 Chrome)，也会发生相同的情况。当用户代理被错误格式化时，还是会返回后备验证码。

**屏幕分辨率和鼠标**

我们尝试了各种屏幕分辨率的组合和各种鼠标的行为配置 (指针的移动速度和模式)。这些对风险分析系统的判断没有任何影响。

## 2.3 网站限制

如果能够解决在我们控制的网站 (attacker.com) 上验证码，但又将 token 与目标网站 (example.com) 相关联起来，这样就能增加攻击的命中率。如此一来，验证码破解服务可以创造有效的 token 并售卖给他人，从而减少网络活动量，达到减少攻击成本的目的。这种简洁明了的点击劫持攻击已被证实 [6]。为了防止攻击，reCaptcha 被重新设计，使得 token 被绑定到发出验证码的网站。除了检查 `Referrer`，该控件通过 `document.location.hostname` 来标识网站，该名称是只读的，不可能因为安全原因被拦截。我们提出了绕过此限制的解决方法。我们在我们的服务器上设置一个虚拟主机，并将 ServerName 和其他必要的字段设置为与 example.com 相对应。通过使用 `a2ensite`，并修改 host 文件，我们可以在本地虚拟主机上运行我们的网站，通过欺骗 reCaptcha 来把我们的请求关联到 example.com。为了完成我们的攻击，我们还需要发送目标网站的 `sitekey`，该 `sitekey` 可以在网页的源代码来中轻易找到。

# 3 简易的验证码破解器

目的是创建出看起来像是合法用户而不是自动机器人生成的 cookie。每一次，我们都在干净的虚拟机中创建一个 cookie，虚拟机的浏览器自动系统没有存储 google.com 上任何账号的 cookie。

## 3.1 获取 token

网站是否会禁止从单个 IP 地址获取大量的 cookie，我们也探讨了这一点。我们可以在一天内创建超过 63,000 个 cookie，而不会触发任何机制或被阻止，并且这个数字的瓶颈仅在于机器的物理硬件性能。这表示没有机制禁止从单个 IP 地址获取大量 cookie。我们检测到的唯一的限制是大量并发请求 (比如说：检测到 DoS 攻击)。事实上，由于以前没有任何攻击是依赖大规模创建 cookie，所以缺乏这方面的保护措施。事实上，我们提出了一种滥用追踪 cookie 的新特性，这将成为攻击者的法宝。

## 3.2 评估

接下来，我们在这些 cookie “成熟” 之后部署我们的系统，以确定在一天内我们可以解决多少个复选框验证码。我们尝试了不同的验证码请求频率，随着请求频率上升，我们观察到准确率呈下降趋势。最后，尽管系统被阻塞了一小段时间，但是在最佳请求频率下，我们每小时收到大约 2,500 个复选框，最高请求频率下，下降到约 1,200。 在平日，我们的结果在 52,000 和 55,000 之间。周末阻塞较少，所以每天获得超过 59,000 个复选框验证码。

# 4 图像验证码

在本节中，我们将探讨新的 Google 图像验证码，并介绍我们在测试过程中观察到的各种特征。攻击者在解决图像验证码时可以利用的一些特征，来解决它，我们的目的就是发掘出这些可能被理由的特征。

## 4.1 图像验证码的灵活性

我们将探讨 reCaptcha 是否具有灵活性，在判断验证码方案是否正确的时候。在任何情况下，在发送响应回复之前必须至少选择两个图像。我们手动地尝试使用不同数量的正确 (n) 和错误 (k) 组合解决图像验证码。在大多数情况下 (74％) 我们发现正确候选图像的数量为 2；其余的包含 3，我们也发现了两个验证码需要选择 4 个。表 4，我们的实验表明，即使少选一个正确答案，或者多选一个错误答案，用户也可以通过检测。基于这些结果，我们设置了我们的验证码破解系统，为解决方案选择 3 个图像；这个策略在 n = 2 时为我们提供了一个可接受误差，并且可能会落在剩余的验证图像的 “放松” 限制之内。

最终，在实践中，结果验证了我们策略的正确性，但是接受挑战的接受组合可能更加灵活，表 4。显示了我们发现始终成立的组合方式。

<center><strong>表 4. 通过图像 reCaptcha 的组合情况</strong></center>

|        Image Selection        | Constraint | Pass |
| :---------------------------: | :--------: | :--: |
|    *n* Correct + *k* Wrong    |  *k* ≤ 1   |  ✔   |
|       (*n* - 1) Correct       |  *n* > 2   |  ✔   |
| (*n* - 1) Correct + *k* Wrong |  *k* > 0   |  ✘   |

## 4.2 重复的图像

在我们的实验中，我们遇到了几种情况，重复的验证码。有时会遇到完全相同的验证码：图像和它们的顺序在两个验证码中是完全相同的。这表明，验证码并不是 “实时” 演算出来的而是从定期更新的相对较小的验证码库中选出的。

我们还发现，验证码之间的图像部分也会交错出现。不过，在大多数情况下，它们具有不同的 MD5 值。因此，我们使用*感知哈希*进行比较，即使它们具有不同的 MD5 值，也可以确定相同的相似性。在所有情况下，我们检测到的图像似乎在视觉上相同。我们认定 20％ 是重复图像。最多被使用的候选图像重复了 12 次。

# 5 图像验证码破解器

近来计算机视觉领域的进步已经取得了非凡的成果 [7, 8, 9, 10]，并且已经出现了利用这些技术的图像注释服务。由于这些服务有效性和适用面大大提升，我们将探讨是否可以将其用于解决图像验证码。

为了解决图像验证码，我们的系统必须自动识别哪些给定的图像在语义上类似于样本图像。在接收到验证码后，我们提取样本和候选图像，以及描述样本图像内容 (例如 “葡萄酒”) 的提示。接下来，所有图像都传递给图像注释模块。

## 5.1 图像注释服务与库

有几个免费的在线服务和库提供功能，通过对提供的无描述图像分配标签 (关键字) 后进行分类。示例输出如表 5 所示。

**GRIS**

Google Reverse Image Search，由 Krizhevsky 等人 [11] 提供了基于图像进行搜索服务。如果搜索成功，它可能返回图像的 “最佳猜测” 描述 (见图 3) 以及包含图像的网站列表以及该图像的其他可用尺寸。虽然这不是 Google 公共 API 的一部分，但我们确定了搜索网址的格式，因此我们的模块可以复制该功能。当对 9 个候选图像进行反向搜索时，我们还会收集包含图像的网页的页面标题作为一个额外的信息。如果可用，我们还获得每个图像的更高分辨率版本，因为它增加了图像注释模块的准确性。如果返回非英文描述，则通过 Google Translate 的自动语言检测功能将其转换为英文。

<div align="center"><img alt="图 3. Google 反向图像搜索 (GRIS)，用于获取图像的描述" src="http://imgur.com/RZgELgn.png"/></div><center><strong>图 3. Google 反向图像搜索 (GRIS)，用于获取图像的描述</strong></center>

**Clarifai**

建立在 Zeiler 等人的反卷积网络上。[12]，并返回一组描述图像的 20 个标签以及每个标签的确认信用指数。

**Alchemy**

同样是建立在深度学习的基础之上，并提供了一个用于图像识别的 API。对于每个提交的图像，服务返回一组标签和每个标签的确认分数。在我们的实验中，图像最多接收 8 个标签，这些标签往往是特定的 (例如 “葡萄酒”)。

**TDL**

Srivastava 和 Salakhutdinov [10] 利用其深度学习系统发布了一个的可以进行图像分类能力的系统。对于每个图像，返回 8 个带信用指数的标签。

**NeuralTalk**

Karpathy 和 Fei-Fei [8] 开发了 NeuralTalk，一种循环神经网络架构，用于生成图像内容的描述信息。我们将返回的描述拆分成多个单词。

**Caffe**

Jia 等人 [13] 发布了 Caffe，这是一个深入的学习框架，我们也在本地使用它来处理图像。Caffe 返回一组 10 个标签；5 具有最高的信用指数的标签，5 个可信度较低关键字，但可能更像是关键词的标签。

<center><strong>表 5. 每个图像注释模块的输出示例，标签以降序的顺序进行排序</strong></center>

|                                   |      GRIS      |   Alchemy   |                 Clarifai                 |                   TDL                    |                NeuralTalk                |                   Caﬀe                   |
| :-------------------------------: | :------------: | :---------: | :--------------------------------------: | :--------------------------------------: | :--------------------------------------: | :--------------------------------------: |
| ![](http://imgur.com/jaC1MFf.png) | wine and blood | wine, glass | glass, red wine, wine, merlot, liquid, bottle, still, glassware, alcohol, drink, wineglass, beverage, pouring, white wine, cabernet, taste, leaded glass, dining, party, vino | red wine, goblet, wine bottle, punching bag, beer glass, perfume, balloon | a glass of wine sitting on top of a table | red wine, wine, alcohol, drug of abuse, drug, red wine, punching bag, beaker, cocktail shaker, table lamp |

## 5.2 标签分类器

返回的标签并不总是完全符合由 reCaptcha 的验证码给出的描述 (提示)。为了克服这个问题，我们研究 (无监督，自主) 机器学习方法和利用机器学习开发一个可以基于标签子集 “猜测” 图像内容的分类器。特别是，我们选择了 Mikolov 等人提出的 Word2Vec 字向量，[14] 用于确定标签和提示之间的相似性。在我们的分类训练中，我们对每个标签 (候选图像和样本图像) 进行建模和表示，作为向量空间中的一个真实向量。分配给图像的每个标签与正确的提示配对，所有标签和提示都作为模型的输入。一旦分类器训练完成，它可以通过计算相应的候选图像标签和样本图像标签之间的余弦相似度来预测验证码提示和标签的相似性，从而识别出与样本图像标签相关联的候选图像标签子集。因此，我们的分类器能够系统的选择具有相似内容的图像，即使注释系统不返回与给定提示完全匹配的标签。

## 5.3 历史模块

许多图像实际上被重复应用于各种验证码。因此，我们手动创建带有图像的标签数据库及其标签，从收集我们遇到的的验证码。每个图像都用描述内容 (例如猫，汤) 的验证码中提供的提示进行注释。我们还列出了一个 `hint_list`，用于储存我们已经看过的图像标签。

## 5.4 方案

每个模块都会将候选图像分为 3 类：`select`， `discard` 和 `undecided`。首先，我们通过 GRIS 收集所有图像的信息。接下来，如果没有提供提示，我们就会在标签数据库中搜索，看看是否能找到此样本图像的标签。接下来，历史模块会在我们的标签数据库中搜索候选图像标签，如果发现，将其标签与提示进行比较，若匹配成功就将其添加到 `select` 列表中。将剩余的无法匹配的图像与 `hint_list` 中的标签进行进一步比较，若匹配成功就将其添加到 `discard` 列表中。随后，图像注释模块处理所有图像并分配给它们标签。如果其中一个标签与图像标签与样本图像标签提示相匹配就会将其添加到 `select` 列表中。如果它与 `hint_list` 中的标签匹配，则将其添加到 `discard` 列表中。对于我们利用第三方的公共服务和库获取的最佳结果以及网页标题，也进行类似的过程。一旦所有模块完成，系统将处理结果并将结果整合。信息被给予不同的 “权重” (例如，由分析网页标题得到的标签，分得较低的权重) ，这样一来，解决了模块将相同图像分配给不同集合的情况。如果 `select` 中没有足够数量的图像，系统会从 `undecided` 的集合中选择剩余的图像。这可以通过我们的标签分类器，或者通过选择与样本图像最相似的 (即常见的) 标签的图像来完成。

## 5.5 评估

**模拟攻击**

我们在下载资料库中模拟了验证码攻击。图 4 展示了每个模块的准确性和信息类型。在这里，我们使用了测试中生成的 hint_list，但没有使用历史模块或图像标签分类器。

<div align="center"><img alt="图 4. 在模拟攻击中，不同模块与数据的组合对 reCaptcha 图片验证码的攻击精确度" src="http://imgur.com/BdZIUga.png"/></div><center><strong>图 4. 在模拟攻击中，不同模块与数据的组合对 reCaptcha 图片验证码的攻击精确度</strong></center>

如之前表 4 所示，reCaptcha 是非常灵活的，即使我们的选择包含错误的图像，也会被认为是正确的 (通过验证)。因此，我们确定系统选择 3 个图像作为解决方案，以便落入 “放宽” 限制。图 4 中的 Pass Challenge 显示的就是攻击结果。

对于每种模块，在它们基于重合标签挑选图像的时候，给它们设置了一个最低准则；对于 GRIS，它同样需要用到验证码中的样本图像标签和 RIS 返回的最佳标签。总的来说，GRIS 的命中率受限于我们获取到的候选图像的最佳标签的数量。对于其他的模块，最低准则就是挑出来 3。张和样本图像有最相似标签的那些候选图像。当使用样本图像标签，候选图像的最佳标签和网页标题时，Alchemy 模块通过了 49.9% 的验证码，Clarifai 通过了 58%。Caffe 也不差，通过 45.9% 的验证码。多数情况下，样本图像标签起着至关重要的作用，依赖注释系统能提高 1.5% 到 15.5% 的命中率。

我们也探索了如何通过为图像注释模块提供更高分辨率版本的图像来影响攻击的准确性。我们能够从 700 个验证码中自动获得 2,909 张图像的更高分辨率版本。其中 371 是相同的图像。高分辨率图像增加了攻击的成功概率，Alchemy 和 Clarifai 分别通过了 53.4％ 和 61.2％ 的验证码。TDL 不太准确，通过了 45％，而 Caffe 的命中率增长到 49.1％。

我们还衡量了如果忽略验证的灵活性，我们的系统还能否胜任这种攻击。由于在大多数情况下，该解决方案由 2 个图像组成，因此我们调整系统为每个验证码选择 2。个图像。图 4 中的精确解决方案栏提供了结果，我们可以看到，所有的图像注释服务在识别正确的图像方面都非常有效。Clarifai 是最有效的，因为它选择了 40.2％ 的验证码中的精确图像，而 Alchemy 达到 31.5％，Caffe 为 28.3％。

**标签分类器**

为了量化我们的标签分类器在我们的验证码系统中的有效性，我们采用了 10 层迭代的验证方法来对资料库中 700 个标记图像验证码的数据库进行分类测试。在我们的第一个实验中，我们跳过了其他图像选择步骤，仅依靠分类器选择图像。对于每个图像，分类器作为输入提示和标签列表，并返回 “相似性” 得分；我们选择了最高分的 3 张图像。我们的攻击提供了 26.28％ (σ= 7.09) 的精确度，并且通过了 44.71％ (σ= 6.39) 的验证码。在第二个实验中，我们将我们的分类器并入我们的系统中，在从 `undecided` 列表中挑选图片时，使用基于分类器的选择结果，而不是基于近似标签的选择结果。使用分类器时，我们的攻击对 Clarifai 的平均精度达到 66.57％ (σ= 7.53)，提高了约 5.3％。分类器比相似度匹配方法更有效，因为它标识了与每个提示相关联的标签的特定子集，而不是通用标签数量而划分出来的子集进行简单的度量。此外，分类器方式并不影响攻击效率，仅仅多耗废大概 0.025s。

**实时攻击**

为了准确测量我们的攻击精度，我们直接用自动验证码破解器攻击 reCaptcha。我们使用 Clarifai 服务，因为它目前为止表现结果最好。

*标签数据库*。我们创建了一个标记的数据库来减少图像重复带来的影响。我们手动标记从验证码中收集的 3,000 张图像，并为每个图像分配描述内容的标签。我们从我们的 hint_list 中选择了相应的标签。我们使用 pHash 进行比较，因为它非常有效，并允许我们的系统在 3.3s 内将验证码的图像与我们的数据库中所有图像进行比较。

我们针对 2,235 个验证码运行了我们设计的系统，并获得了 70.78％ 的准确性。与模拟实验相比有更高的精度，部分原因是因为图像重复较多；历史模块在我们的标记数据库中识别到了 1,515 个样本图像和 385 个候选图像。

*平均运行时间*。我们的攻击非常有效，破解单个验证码平均耗时 19.2s。最耗时的阶段是运行 GRIS，因为它搜索 Google 中的所有图像并处理结果，包括提取指向更高分辨率版本的图像的链接。

*离线模式*。我们同样评估了离线模式下的攻击，不使用任何的在线注释服务或者 GRIS；仅仅使用本地的库，标签数据库和分类器。一共使用了两个库：NeuralTalk 和 Caffe。当使用 Caffe 和分类器时，我们的系统解决了 41.57% 的图像验证码，单个平均耗时提高到了 20.9s。当使用 NeuralTalk 时，大概解决了 40%，耗时也相当长，达到了 117.8s，因为 NeuralTalk 处理 10 个图像需要 110.9s。不过，利用 GPU 来做计算会提高效率，减少耗时。

因此，攻击者能对 reCaptcha 的图像验证码部署精确有效的攻击，并且不需要依赖外部的服务，这些处理大量图片或报告可疑活动的服务也行不免费。

<div align="center"><img alt="图 5. Facebook 的图片验证码" src="http://imgur.com/nSVewHc.png"/></div><center><strong>图 5. Facebook 的图片验证码</strong></center>

# 6 适用性

我们的攻击的原理也可以应用于其他方案，通过提取图像的语义，我们可以构建对其他基于图像的验证码的攻击，如 Facebook captcha (图 6)。当用户向包含可疑 URL 的其他用户发送消息时，向用户显示图像验证码，他们必须首先传递图像。Facebook 的图像验证码采用与 reCaptcha 相同的方法，用户必须确定哪些图像 (12 张以内) 中具有与给定提示相匹配的内容。然而，有一些差异。 Facebook 以 HTML 动态调整图像大小，允许访问图像的高分辨率版本。此外，没有显示样品图像。该系统有与 reCaptcha 相同的灵活性规则。正确图像的数量从 2 到 10 不等，其中 5 - 7 是最常见的情况。因此，我们调整我们的解算法只能选择包含在 `select` 中的图像，而不是选择特定数量的图像。

对于超过 200 个 Facebook 图片验证码，我们与 Clarifai 的攻击达到了最高的准确率为 83.5％。与 reCaptcha 相比，更高的精度是由于两个特征。首先，候选图像的分辨率越高，其次，创建挑战时使用完全不相关的图像有助于丢弃不正确的选项。另一方面，reCaptcha 选择属于同一类别的图像 (例如，所有都是某种类型的食物)，这使得区分更加困难。

# 7 经济分析

鉴于验证码破解通常源于经济利益，我们从经济角度评估我们的发现，并将我们的攻击视为一种验证码攻击。

## 7.1 图片验证码

将我们的表现与 Decaptcher 最旧的验证码服务比较。我们选择了 Decaptcher 有两个原因。首先，它支持图像 reCaptcha，每解决 1000 个验证码收取 \$2。二，它之前的表现 [15]，证明它是准确度最高的验证码破解服务。

我们将 700 图像验证码提交给 Decaptcher，并测量响应时间和准确性 (考虑到解决方案的灵活性)。有趣的是，Decaptcher 拒绝了我们提交的许多验证码。

由于服务超载，我们的提交的一些验证码被拒绝，并且必须过段时间后重新提交，并收到超时错误，因为解决者在服务分配的时间窗口中没有提供答案。 258 个挑战 (占全部的 36.85％) 是完全匹配的。考虑到灵活性，解决了 321 (44.3％) 的验证码。单个平均的解决时间是 22.5s。随着人们越来越适应图片验证码，人工破解的精确度会随着时间提高，但是不可否认，我们的系统还是一种比较有经济效益的可选方案。*我们的完全离线验证码破解系统在准确度和效率上完全比得上专业的破解服务，尽管如此，我们也不会提供给任何攻击者来获利。*

<center><strong>表 6. 从Decaptcher服务返回的错误</strong></center>

|        Detail         | Out of 700 challenges |
| :-------------------: | :-------------------: |
|       **Error**       |                       |
| System overload error |     147 (21.00%)      |
|     Timeout error     |      88 (12.57%)      |
|      **Success**      |                       |
|      Exact match      |     258 (36.85%)      |
|    Pass challenges    |     321 (44.30%)      |

## 7.2 复选框验证码

假设每解决 1000 个验证码收费 \$2 的话，我们的 token 攻击，一个主机 (IP 地址) 一天，能收入 \$104 到 \$110。通过使用代理服务做并行攻击的话，这个收入的数字会更加可观。

# 道德声明

我们把发现和建议报告给了 Google，帮助他们提高 reCaptcha 对自动攻击的健壮性。根据我们的成果，reCaptcha 改变了安全策略和风险分析过程，来缓解我们的大规模 token 攻击。他们也移除了图片验证码方案的灵活性和样本图片，从而降低了攻击的准确度。我们也通知的 Facebook，但还没有发现他们做任何改变。总之，我们希望通过分享我们的发现，能帮助发起研究者和企业之间对于验证码未来的亟需的讨论。

# 参考文献

[1] L. Von Ahn, B. Maurer, C. McMillen, D. Abraham, and M. Blum, “reCAPTCHA: Human-based character recognition via web security measures,” Science, vol. 321, no. 5895, 2008.

[2] Google Online Security Blog, “Are you a robot? Introducing “No CAPTCHA reCAPTCHA”,” [https://security.googleblog.com/2014/12/are-you-robot-introducing-no-captcha.html](https://security.googleblog.com/2014/12/are-you-robot-introducing-no-captcha.html).

[3] E. Bursztein, J. Aigrain, A. Moscicki, and J. C. Mitchell, “The end is nigh: Generic solving of text-based CAPTCHAs.” in USENIX WOOT ’14.

[4] I. J. Goodfellow, Y. Bulatov, J. Ibarz, S. Arnoud, and V. Shet, “Multi-digit number recognition from street view imagery using deep convolutional neural networks,” in CoRR ’13.

[5] K. Mowery and H. Shacham, “Pixel perfect: Fingerprinting canvas in html5,” in W2SP ’12.

[6] E. Homakov. The No CAPTCHA problem. [http://homakov.blogspot.in/2014/12/the-no-captcha-problem.html](http://homakov.blogspot.in/2014/12/the-no-captcha-problem.html).

[7] O. Vinyals, A. Toshev, S. Bengio, and D. Erhan, “Show and tell: A neural image caption generator,” in CoRR ’14.

[8] A. Karpathy and L. Fei-Fei, “Deep visual-semantic alignments for generating image descriptions,” in CoRR ’14.

[9] M. M. Kalayeh, H. Idrees, and M. Shah, “NMF-KNN: Image Annotation Using Weighted Multi-view Non-negative Matrix Factorization,” in CVPR ’14.

[10] N. Srivastava and R. Salakhutdinov, “Multimodal learning with deep boltzmann machines,” Journal of Machine Learning Research, vol. 15, pp. 2949–2980, 2014.

[11] A. Krizhevsky, I. Sutskever, and G. E. Hinton, “Imagenet classiﬁcation with deep convolutional neural networks,” in NIPS ’12.

[12] M. D. Zeiler, G. W. Taylor, and R. Fergus, “Adaptive deconvolutional networks for mid and high level feature learning,” in ICCV ’11.

[13] Y. Jia, E. Shelhamer, J. Donahue, S. Karayev, J. Long, R. Girshick, S. Guadarrama, and T. Darrell, “Caffe: Convolutional architecture for fast feature embedding.”

[14] T. Mikolov, K. Chen, G. Corrado, and J. Dean, “Efﬁcient estimation of word representations in vector space,” in CoRR ’13.

[15] M. Motoyama, K. Levchenko, C. Kanich, D. McCoy, G. M. Voelker, and S. Savage, “Re: CAPTCHAs: understanding captcha-solving services in an economic context,” in USENIX Security ’10.