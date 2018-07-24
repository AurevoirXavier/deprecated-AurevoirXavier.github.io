---
layout: post
title: "No module named 'RPi.GPIO'"
date:   2017-08-14
excerpt: "ArchLinux 下安装树莓派的 GPIO 库"
tags: [ArchLinux, raspberryPi]
comments: true
---

<center><h2>在 ArchLinux 下安装树莓派的 GPIO 库</h2></center>

<!--more-->

根据你的 **Python** 版本安装对应的工具链，例如 `python2-setuptools`  `python2-pip,`  `python-setuptools` `python-pip`。

安装完成后，就可以利用 **pip** 来安装 **RPI.GPIO**。

总的来说就是这样：

```sh
sudo pacman -S python-setuptools python-pip

sudo pip install RPI.GPIO
```
