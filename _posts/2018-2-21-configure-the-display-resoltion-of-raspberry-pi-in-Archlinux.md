---
layout: post
title: "configure the display resoltion of raspberryPi on ArchLinux"
date:   2018-02-21
excerpt: "ArchLinux 下配置树莓派的输出分辨率"
tags: [ArchLinux, raspberryPi]
comments: true
---

<center><h2>ArchLinux 下配置树莓派的输出分辨率</h2></center>

<!--more-->

**需要权限来做修改：**

```sh
$ vi /boot/config.txt 
```

**可选模式（可以不设置）：**

`sdtv_mode=0` - NTSC signal (AMERICA)

`sdtv_mode=1` - Japanese NTSC signal

`sdtv_mode=2` - PAL signal (EUROPE and ASIA)

`sdtv_mode=3` - Brazilian PAL signal

**可选长宽比（可以不设置）：**

`sdtv_aspect=1` - 4:3 aspect ratio

`sdtv_aspect=2` - 14:9 aspect ratio

`sdtv_aspect=3` - 16:9 aspect ratio

**可选 hdmi 类型：**

`hdmi_group=0` - 树莓派自动检测

`hdmi_group=1` - 高清电视

`hdmi_group=2` - 电脑显示器

**可选 hdmi 模式（注意：与你上面的选择有关）：**

1 - 如果选择了高清电视：

<div align="center"><img alt="hdmi_group=1" src="https://i.imgur.com/dCUwpnZ.png"/></div>

<div align="center"><img alt="hdmi_group=1" src="https://i.imgur.com/B0BFspZ.png"/></div>

<div align="center"><img alt="hdmi_group=1" src="https://i.imgur.com/44JCdxX.png"/></div>

2 - 如果选择了电脑显示器：

<div align="center"><img alt="hdmi_group=2" src="https://i.imgur.com/l9vQnDB.png"/></div>

<div align="center"><img alt="hdmi_group=2" src="https://i.imgur.com/EGoSqSk.png"/></div>

<div align="center"><img alt="hdmi_group=2" src="https://i.imgur.com/bsfr4UJ.png"/></div>

<div align="center"><img alt="hdmi_group=2" src="https://i.imgur.com/FroEvqN.png"/></div>

**帧颜色深度（可以不设置）：**

`framebuffer_depth=8`

`framebuffer_depth=16`

`framebuffer_depth=24`

`framebuffer_depth=32`

---

下面贴上我个人的设置：

```sh
hdmi_group=2

hdmi_mode=82

framebuffer_depth=32
```