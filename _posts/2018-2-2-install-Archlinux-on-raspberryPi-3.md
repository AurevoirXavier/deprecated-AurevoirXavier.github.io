---
layout: post
title: "Install ArchLinux on raspberryPI 3"
date:   2018-02-02
excerpt: "Raspberry PI 3 安装 ArchLinux"
tags: [ArchLinux, raspberryPi]
comments: true
---

<center><h2>Raspberry PI 3 安装 ArchLinux</h2></center>

<!--more-->

首先说明本教材需要一台 **Linux** 机器。*OSX，Windows* 都不行。如果没有现成的，那么虚拟机是一个好选择。

配置系统：

```sh
# 列出当前设备
$ lsblk

# 使用 fdisk 分区
$ sudo fdisk /dev/sdX
# 清除分区，输入：（o）
# 新建第一个分区，输入：（n，p，enter，enter，+100m，t，c）
# 新建第二个分区，输入：（n，p，enter，enter，enter）
# 写入更改，输入：（w）

# 设置一号分区格式，可能需要安装 dosfstools
$ sudo mkfs.vfat /dev/sdX1

$ sudo mkdir /mnt/boot

$ sudo mount /dev/sdX1 /mnt/boot

# 设置二号分区格式，可能需要安装 f2fs-tools
$ sudo mkfs.f2fs /dev/sdX2

$ sudo mkdir /mnt/root

$ sudo mount -t f2fs /dev/sdX2 /mnt/root

$ wget http://archlinuxarm.org/os/ArchLinuxARM-rpi-2-latest.tar.gz

# 下面需要 root 用户，用 sudo 是不可行的。详见官网：https://archlinuxarm.org/platforms/armv8/broadcom/raspberry-pi-3
$ su

$ tar xvzf ArchLinuxARM-rpi-2-latest.tar.gz -C /mnt/root

$ sync

$ mv /mnt/root/boot/* /mnt/boot

$ vi /mnt/root/etc/fstab
# 添加以下内容：
/dev/mmcblk0p2 / f2fs defaults,noatime,discard 0 0
tmpfs   /tmp     tmpfs   nodev,nosuid,size=2G  0 0

$ /mnt/boot/cmdline.txt
# 添加以下内容：
rootfstype=f2fs

$ cp /mnt/root/bin/true /mnt/root/sbin/fsck.f2fs

$ vi /mnt/boot/config.txt
# 添加以下内容：
dtparam=audio=on
hdmi_drive=2
# 如果你的 sd 卡速度是 class 10 级别的可以追加这一条：
dtparam=sd_overclock=100

$ umount /mnt/boot /mnt/root
```

下面可以把 sd 卡插入 *Raspberry PI* 中了。

初始化配置：

```sh
# 多种登录方式，这里我选择 ssh，address 替换为你的 Raspberry PI 地址
ssh alarm@address

su

pacman-key --init

# 在执行这一条命令之前也许你需要修改一下 /etc/pacman.d/mirrorlist 里面的源以达到最佳速度，建议不是台湾或者新加坡的全部删掉
pacman -Syu

# 修改语言
sudo vi /etc/locale.gen
# 去掉你想要的一项的前面的注释符号，这里我选择：
en_US.UTF-8 UTF-8

sudo locale-gen

sudo vi /etc/profile
# 添加想要的语言，这里我选择：
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8
```

至此基本配置完成。如果不满意 alarm 这个用户名或者 alarmpi 这个主机名，可以参考我的另外一篇[文章](https://uvwvu.xyz/ArchLinux/change-username-and-hostname-on-ArchLinux.rs)来做修改。