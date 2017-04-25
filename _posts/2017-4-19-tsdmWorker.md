---
layout: post
title: "Tsdm Worker"
date:   2017-04-19
excerpt: "天使动漫一键打工脚本"
project:    true
tags: [js, html]
comments: true
---

<h1><center><a href="https://github.com/AurevoirXavier/TsdmWorker">TsdmWorker.js</a></center></h1>

下载 TsdmWorker.user.js 后，拖入 Tampermonkey 内即可使用。

如不能拖入，右键编辑或者在 github 里直接点开，复制（一定要复制完整）粘贴源代码进 Tampermonkey 即可。

有坛友反应不能使用，原因在于你的网速过慢，你还没有加载完页面，我的脚本就执行了，实际上页面里面检测你点击了多少广告数的脚本并没有开始计数。请结合自身网速条件更改我脚本中的两个 0 单位是毫秒。第一个 0 多久时间开始点击广告，第二个 0 是多久时间开始点击领取奖励。(第二个数值必须大于等于第一个数值因为是同步执行的，第二个等待时间会从第一个等待时间开始计算)

图解：

<div align="center"><img alt="" src="http://i.imgur.com/k1bqetR.gif"/></div>

<br>

<div align="center"><img alt="" src="http://i.imgur.com/4t9YDMR.gif"/></div>

<br>

<div align="center"><img alt="" src="http://i.imgur.com/xGQH1Pk.gif"/></div>