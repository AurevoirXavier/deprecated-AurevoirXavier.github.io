---
layout: post
title: "I’m not a human: Breaking the Google reCAPTCHA"
date:   2017-04-19
excerpt: "Google reCAPTCHA 验证机制"
tags: [program, google, captcha]
comments: true
---

---

<center><h1 style="">我虽非人类：且看我如何攻破 Google reCAPTCHA</h1></center>

<center><strong>Aurevoir Xavier 译</strong></center>

<center><h2><i>Suphannee Sivakorn, Jason Polakis, and Angelos D. Keromytis</i></h2></center>

<center><i>[suphannee, polakis, angelos]@cs.columbia.edu Columbia University, New York NY, USA</i></center>

---

自从验证码被创造出来那一天，就广泛地运用于阻止攻击者的不合法操作。尽管验证码能在一定程度上拦截恶意攻击者，但是在经济利益的诱惑下，各种针对验证码的自动化攻击方式如雨后春笋般冒出，那么验证码服务也就相应地做出改进。然而近来，出现了一种针对文本验证码的新型且通用攻击方式。Google 也适时地公布了 reCaptcha 的最新版本。最新版本有两个目标：一是减少合法用户通过验证码认证的成本 (省时省力)，二是提供了对计算机来说，比文本识别更有难度的验证码。ReCaptcha 是由一个 “高级的风险分析系统” 驱动的，这种系统通过分析收到的请求，挑出适合难度的验证码返回给用户。用户可能需要勾选一个复选框，或者需要挑出描述相同内容的一组图片。

在这篇论文中，我们对 reCaptcha 和多种多样的用户请求是如何影响风险分析系统做判断，做了系统研究。通过大量的实验，我们发现一些缺陷，攻击者可以通过这些缺陷来轻松地影响风险分析系统，绕过验证码限制，进而实施大规模的攻击。随后，我们利用深度学习技术进行图像的语义注释，设计了一种新颖的低成本攻击方式。我们的攻击系统非常有效，能够自动解决 70.78% 的图片 reCaptcha，每个验证码的认证只平均只耗费 19 秒。我们对 Facebook 的图片验证码也做了测试攻击，成功率达到了 83.5%。基于我们的实验所得，我们针对这些攻击，提供了一系列的保护和改善措施。总之，我们的研究专注于 reCaptcha，这些发现有非常广的影响。因为对图片所传达的语义信息的逻辑自动化处理越来越多，越来越频繁，所以，验证码也必然要顺应趋势，在更新奇的方向上做更深的探索。

## 1 了解 reCaptcha

Google 提供的 reCaptcha 服务 [1] 是最广泛使用的验证码服务，已被许多流行网站采用，用于防止自动漫游器进行恶意活动。Google 宣布 [2] 部署了一个新的 reCaptcha 机制，旨在使其更加人性化和安全。

**网页控件**

当访问由 reCaptcha 保护的网页时，会显示一个小的网页控件 (如图 1 (a) 所示)。这个控件的 JavaScript 代码被模糊化，为了防止被第三方分析。当它加载时，会收集有关用户浏览器的信息并将其发送回服务器。此外，它会执行一系列检查以核实用户的浏览器。

**工作流程**

一旦用户点击了复选框，就会向 Google 发送一个请求，其中包括 (i) Referrer，(ii) 网站的 sitekey (在注册 reCaptcha 时获得)，(iii) 提供给 google.com 的 cookie，以及 (iv) 由执行此控件的浏览器生成的信息检查 (加密)。然后由先进的风险分析系统分析该请求，最后决定向用户呈现哪种类型的验证码。

<div><div align="center"><img alt="(a) 用户点击复选框之前" src="http://imgur.com/eHshegQ.png"/></div><center>(a) 用户点击复选框之前</center><div align="center"><img alt="(b) 用户点击复选框之后" src="http://imgur.com/OjqRJCz.png"/></div><center>(b) 用户点击复选框之后</center></div><center><strong>图 1. reCaptcha 网页控件</strong></center>



<br>



<div align="center"><img alt="reCaptcha 网页控件" src="http://imgur.com/bejOjrz.png"/></div><center><strong>图 2. reCaptcha 提供的相似图片验证码</strong></center>

**验证码类型**

验证码类型类型因用户而异。如果用户的特定某信用较低，频繁请求或多次回答错误，将会提高验证码的难度。在我们的实验中，我们遇到了以下版本的 reCaptcha：

- ​“无验证码的 reCaptcha” [图 1]。新的用户友好版本，旨在彻底消除解决问题的困难。单击控件的复选框，如果高级风险分析系统认为用户具有很高的信用度，那么验证通过，用户不需要任何操作。对于本文的其余部分，我们将这种类型的验证码统称为复选框验证码。
- 图片 reCaptcha [图 2]。这个新版本是建立在识别具有相似内容的图像的概念上。其包含示例图像和 9 个候选图像，要求用户选择与样本相似的图像。验证码通常会包含描述用户需要选择的图像内容的关键字 (对图片内容的概括性描述)。正确图像的数量一般在 2 和 4 之间。
- 文本reCaptcha [表 1 (a) 至 (e)]。当高级风险分析考虑到用户的信用较低时，将会提供这些扭曲的文字来 (文本验证码)。在用户点击复选框之前，如果用户机器在浏览器的某些检查中失败了，那么分析系统就会返回给用户类似 (e) 这种可靠的验证码，网页控件会自动收取并显示此验证码。在接下来 6 个月的时间里，文字识别码似乎逐渐被淘汰，图像验证码现在是默认的返回类型，因为机器人反而更容易解决这些验证码 [3, 4] 。

<center><strong>表 1. 文本 reCaptcha 的一些例子</strong></center>

|     (a) | ![](http://imgur.com/rDE98fd.png) |     (b) | ![](http://imgur.com/w7oBpZG.png) |
| ------: | :-------------------------------- | ------: | :-------------------------------- |
| **(c)** | ![](http://imgur.com/Q7weiAs.png) | **(d)** | ![](http://imgur.com/YyemWJV.png) |
| **(e)** | ![](http://imgur.com/D3cyxkI.png) |         |                                   |

**解决方案**

一旦验证码对用户展示出来，它必须在 55 秒内被回答。否则，用户需要再次单击该复选框以接收新的验证码。一旦用户点击，一个名为 recaptcha-token 的 HTML 字段就用会被储存到 token 中。如果用户被判定是合法的，不需要验证码验证，则该 token 在 Google 服务器获取认可。当完成所需的操作时，token 将提交给网站，用于获取认可。网站通过 reCaptcha API 发送验证请求，该 API 包含： (i) 共享密钥，(ii) 响应令牌，以及 (iii)用户的 IP 地址。若收到这个请求的响应，说明认证成功。

## 2 剖析风险分析系统

在本节中，我们将探讨 Google 的高级先进风险分析体系，并确定用户和用户浏览器信息的各种特征值是如何影响其工作的。我们遵循黑盒测试方法来确定系统和测试环境的不同方面是如何影响风险分析过程的。我们的目的是发出由高级风险分析系统认定为合法的验证码，如此一来，我们就能获得最简单的只需按一下就能通过验证的复选框验证码。

**2.1 浏览历史**

Google 的跟踪 cookie 在确定应该向用户呈现何种难度的验证码这一方面方面起着至关重要的作用。我们构建了实验，旨在量化一个特定 cookie 所需的最低浏览历史数量，根据这些 cookie 对合法用户呈现一个复选框验证码。我们探索了多重网络连接设置以及生成浏览历史的活动。例如在我们的分网和美国出口节点的 Tor 网频进行实验。我们自动搜索 Google 的某些关键词，访问搜索出来的链接，观看 Youtube 上的视频，Google 地图上的搜索，访问包含 Google+ 插件和控件的热门网站。令人惊讶的是，我们可以在 cookie 创建后的第 9 天开始时获得一个复选框验证码，而不需要任何浏览活动和网络连接类型，如表 2 所示。我们的实验还显示，每个 cookie 最多可以收到 8 个复选框验证码在一天之内。

<center><strong>表 2. 构造追踪 cookie 和 “模拟” 用户行为</strong></center>

|   Network    | Web Surfing | Account |  Threshold  |
| :----------: | :---------: | :-----: | :---------: |
| Departmental |  Frequent   |   No    |   9th day   |
| Departmental |  Moderate   |   No    |   9th day   |
|     ToR      |  Frequent   |   No    |   9th day   |
|     ToR      |  Moderate   |   No    |   9th day   |
|   **Any**    |  **None**   | **No**  | **9th day** |

**2.2 浏览器环境**

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

为了确定用户代理如何影响用户的信用度，我们按特定的情况给其分组。我们发现，如果用户代理包含过时版本的浏览器或浏览器引擎，则控件会自动将环境视为可疑环境，并为用户提供一个后备验证码 (表1 - (e))。如果浏览器和引擎版本是最新的，但是不符合实验的实际环境 (例如，如果我们使用 Firefox，但报告 Chrome），也会发生相同的情况。当用户代理被错误格式化时，还是会返回后备验证码。

**屏幕分辨率和鼠标**

我们尝试了各种屏幕分辨率的组合和各种鼠标的行为配置 (指针的移动速度和模式)。这些对风险分析系统的判断没有任何影响。

**2.3 网站限制**

如果能够解决在我们控制的网站 (attacker.com) 上验证码，但又将 token 与目标网站 (example.com) 相关联起来，这样就能增加攻击的命中率。如此一来，验证码破解服务可以创造有效的 token 并售卖给他人，从而减少网络活动量，达到减少攻击成本的目的。这种简洁明了的点击劫持攻击已被证实 [6]。为了防止攻击，reCaptcha 被重新设计，使得 token 被绑定到发出验证码的网站。除了检查 Referrer，该控件通过 document.location.hostname 来标识网站，该名称是只读的，不可能因为安全原因被拦截。我们提出了绕过此限制的解决方法。我们在我们的服务器上设置一个虚拟主机，并将 ServerName 和其他必要的字段设置为与 example.com 相对应。通过使用 a2ensite，并修改 host 文件，我们可以在本地虚拟主机上运行我们的网站，通过欺骗 reCaptcha 来把我们的请求关联到 example.com。为了完成我们的攻击，我们还需要发送目标网站的 sitekey，sitekey 可以在网页的源代码来中轻易找到。

## 3 简易的验证码破解器

目的是创建出看起来像是合法用户而不是自动机器人生成的 cookie。每一次，我们都在干净的虚拟机中创建一个 cookie，虚拟机的浏览器自动系统没有存储 google.com 上任何账号的 cookie。

**3.1 获取 token

网站是否会禁止从单个 IP 地址获取大量的 cookie，我们也探讨了这一点。我们可以在一天内创建超过 63,000 个 cookie，而不会触发任何机制或被阻止，并且这个数字的瓶颈仅在于机器的物理硬件性能。这表示没有机制禁止从单个 IP 地址获取大量 cookie。我们检测到的唯一的限制是大量并发请求 (比如说：检测到 DoS 攻击)。事实上，由于以前没有任何攻击是依赖大规模创建 cookie，所以缺乏这方面的保护措施。事实上，我们提出了一种滥用追踪 cookie 的新特性，这将成为攻击者的法宝。

**3.2 评估**

接下来，我们在这些 cookie “成熟” 之后部署我们的系统，以确定在一天内我们可以解决多少个复选框验证码。我们尝试了不同的验证码请求频率，随着请求频率上升，我们观察到准确率呈下降趋势。最后，尽管系统被阻塞了一小段时间，但是在最佳请求频率下，我们每小时收到大约 2,500 个复选框，最高请求频率下，下降到约 1,200。 在平日，我们的结果在 52,000 和 55,000 之间。周末阻塞较少，所以每天获得超过 59,000 个复选框验证码。

## 4 图片验证码

在本节中，我们将探讨新的 Google 图像验证码，并介绍我们在测试过程中观察到的各种特征。攻击者在解决图像验证码时可以利用的一些特征，来解决它，我们的目的就是发掘出这些可能被理由的特征。

**4.1 图片验证码的灵活性**

我们将探讨 reCaptcha 是否具有灵活性，在判断验证码方案是否正确的时候。在任何情况下，在发送响应回复之前必须至少选择两个图像。我们手动地尝试使用不同数量的正确 (n) 和错误 (k) 组合解决图像验证码。在大多数情况下 (74％) 我们发现正确候选图像的数量为 2；其余的包含 3，我们也发现了两个验证码需要选择 4 个。表 4，我们的实验表明，即使少选一个正确答案，或者多选一个错误答案，用户也可以通过检测。基于这些结果，我们设置了我们的验证码破解系统，为解决方案选择 3 个图像；这个策略在 n = 2 时为我们提供了一个可接受误差，并且可能会落在剩余的验证图像的 “放松” 限制之内。

最终，在实践中，结果验证了我们策略的正确性，但是接受挑战的接受组合可能更加灵活，表 4。显示了我们发现始终成立的组合方式。

|        Image Selection        | Constraint | Pass |
| :---------------------------: | :--------: | :--: |
|    *n* Correct + *k* Wrong    |  *k* ≤ 1   |  ✔   |
|       (*n* - 1) Correct       |  *n* > 2   |  ✔   |
| (*n* - 1) Correct + *k* Wrong |  *k* > 0   |  ✘   |