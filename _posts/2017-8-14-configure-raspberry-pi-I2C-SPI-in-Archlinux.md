---
layout: post
title: "Configure raspberry's I2C and SPI in Archlinux"
date:   2017-08-14
excerpt: "在 Archlinux 下配置树莓派的 I2C SPI"
tags: [Archlinux, raspberry, program]
comments: true
---

首先本人的树莓派型号为`树莓派3b+`。

**Part I** 为启用 **I2C**，如果还需要使用 **SPI**，请看 **Part II**。

##Part I

**第一步**

修改 `/etc/modules-load.d/raspberrypi.conf` (若不存在此文件请自行手动创建)。向其中添加下列代码：

```
i2c-bcm2708

i2c-dev
```

**第二步**

修改  `/boot/config.txt`  (若不存在此文件请自行手动创建)。向其中添加下列代码：

```
device_tree_param=i2c1=on

device_tree_param=i2c_arm=on
```

重启后，在 `/dev` 看到对应的设备文件说明成功。也可以执行 `i2cdetect -y 1`。

---

##Part II

**第一步**

修改 `/etc/modules-load.d/raspberrypi.conf` (若不存在此文件请自行手动创建)。向其中添加下列代码：

```
i2c-bcm2708

i2c-dev

spi-bcm2708
```

**第二步**

```
device_tree_param=i2c1=on

device_tree_param=i2c_arm=on

device_tree_param=spi=on
```

重启后，在 `/dev` 看到对应的设备文件说明成功。也可以执行 `i2cdetect -y 1`。