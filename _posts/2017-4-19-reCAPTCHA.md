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

自从验证码被创造出来那一天，就广泛地运用语阻止攻击者的不合法操作。尽管验证码能在一定程度上拦截恶意攻击者，但是在经济利益的诱惑下，各种针对验证码的自动化攻击方式如雨后春笋般冒出，那么验证码服务也就相应地做出改进。然而近来，出现了一种针对文本验证码的新型且通用攻击方式。Google 也适时地公布了 reCaptcha 的最新版本。最新版本有两个目标：一是减少合法用户通过验证码认证的成本（省时省力），二是提供了对计算机来说，比文本识别更有难度的验证码。ReCaptcha 是由一个 “高级的风险分析系统” 驱动的，这种系统通过分析收到的请求，挑出适合难度的验证码返回给用户。用户可能需要勾选一个复选框，或者需要挑出描述相同内容的一组图片。

在这篇论文中，我们对 reCaptcha 和多种多样的用户请求是如何影响风险分析系统做判断，做了系统研究。通过大量的实验，我们发现一些缺陷，攻击者可以通过这些缺陷来轻松地影响风险分析系统，绕过验证码限制，进而实施大规模的攻击。随后，我们利用深度学习技术进行图像的语义注释，设计了一种新颖的低成本攻击方式。我们的攻击系统非常有效，能够自动解决 70.78% 的图片 reCaptcha，每个验证码的认证只平均只耗费 19 秒。我们对 Facebook 的图片验证码也做了测试攻击，成功率达到了 83.5%。基于我们的实验所得，我们针对这些攻击，提供了一系列的保护和改善措施。总之，我们的研究专注于 reCaptcha，这些发现有非常广的影响。因为对图片所传达的语义信息的逻辑自动化处理越来越多，越来越频繁，所以，验证码也必然要顺应趋势，在更新奇的方向上做更深的探索。

## 了解 Recaptcha

Google 提供的 reCaptcha 服务[1]是最广泛使用的验证码服务，已被许多流行网站采用，用于防止自动漫游器进行恶意活动。Google 宣布[2]部署了一个新的 reCaptcha 机制，旨在使其更加人性化和安全。

**网页控件**

当访问由 reCaptcha 保护的网页时，会显示一个小的网页控件 (如图1(a) 所示)。这个控件的 JavaScript 代码被模糊化，为了防止被第三方分析。当它加载时，会收集有关用户浏览器的信息并将其发送回服务器。此外，它会执行一系列检查以核实用户的浏览器。

## 工作流程

一旦用户点击了复选框，就会向 Google 发送一个请求，其中包括 (i) Referrer，(ii) 网站的 sitekey (在注册 reCaptcha 时获得)，(iii) 提供给 google.com 的 cookie，以及 (iv) 由执行此控件的浏览器生成的信息检查 (加密)。然后由先进的风险分析系统分析该请求，最后决定向用户呈现哪种类型的验证码。

<div><div align="center"><img alt="(a) 用户点击复选框之前" src="http://imgur.com/eHshegQ.png"/></div><center>(a) 用户点击复选框之前</center><div align="center"><img alt="(b) 用户点击复选框之后" src="http://imgur.com/OjqRJCz.png"/></div><center>(b) 用户点击复选框之后</center></div>

<center><strong>图 1. reCaptcha 网页控件</strong></center>

<div align="center"><img alt="reCaptcha 网页控件" src="http://imgur.com/bejOjrz.png"/></div><center>reCaptcha 网页控件</center>