---
1layout: post
title: "how to install ArchLinux"
date:   2018-06-27
excerpt: "如何安装 ArchLinux"
tags: [ArchLinux]
comments: true
---

<center><h2>如何安装 ArchLinux</h2></center>

<!--more-->

*当年入坑 **ArchLinux** 因为其炫酷的 logo 以及极高的定制性，不过这极高的定制性也是让新手吃尽苦头。今天碰巧重装，那么大致步骤为大家双手奉上：*

*虚拟机或实体机加载镜像文件进入安装界面这我就不多废话了，假设你已经进入了安装界面（命令行界面 `root@archiso ~ #`），后面的 `root@archiso ~ #` 我会用 `$` 来代替*。

### 1. 配置 ssh（可选）：

`ssh` 之后可以在自己的终端进行操作即方便又美观，何乐而不为？

```sh
# 远程连接 root 用户需要修改一下保护机制，vi 可替换为任意你喜欢的编辑器
$ vi /etc/ssh/sshd_config

# 将光标移到文件末尾，加上下面两行
# 允许 root 用户登陆
PermitRootLogin yes
# 允许空密码登陆
PermitEmptyPasswords yes

# 重启 sshd 服务，使上面的改变生效
$ systemctl restart sshd

# 查看当前机器 ip
$ ifconfig
```

经过上面的步骤现在你可以 `ssh root@{你刚查到的ip}`，比如我 `ssh root@192.168.123.27`。

### 2. 分区：

输入 `$ ls /sys/firmware/efi/efivars` 如果提示目录不存在，那么咱们进入 **BIOS** 启动方式分支。

##### BIOS 启动方式：

```sh
# 查看驱动器情况
$ lsblk

# 根据上面结果选择你要安装的分区
$ gdisk /dev/sda

# 新建分区，n 就是 new 的意思
Command (? for help): n
# 分区编号，我这里选择回车默认为 1
Partition number (1-128, default 1): 
# 区块起点，我同样直接回车使用默认值
First sector (xxx, default = xxx) or {+-}size{KMGTP}:
# 区块终点 +1007k 如此一来分配了一个大小 1007k 的空间（官方要求的大小）
Last sector (xxx-xxx, default = xxx) or {+-}size{KMGTP}: +1007k
# 分区类型，ef02 BIOS boot partition，输入 l 可以看到类型表
Hex code or GUID (L to show codes, Enter = 8300): ef02
# 接着我们分配引导分区，只有大小类型与启动分区不同
Partition number (2-128, default 2):
First sector (xxx-xxx, default = xxx) or {+-}size{KMGTP}:
Last sector (xxx-xxx, default = xxx) or {+-}size{KMGTP}: +200m
Hex code or GUID (L to show codes, Enter = 8300):
# 一鼓作气，分配交换分区
Partition number (3-128, default 3):
First sector (xxx-xxx, default = xxx) or {+-}size{KMGTP}:
Last sector (xxx-xxx, default = xxx) or {+-}size{KMGTP}: +2g
Hex code or GUID (L to show codes, Enter = 8300): 8200
# 有了上面的基础最后一个根分区，一路回车
Partition number (4-128, default 4):
First sector (xxx-xxx, default = xxx) or {+-}size{KMGTP}:
Last sector (xxx-xxx, default = xxx) or {+-}size{KMGTP}:
Hex code or GUID (L to show codes, Enter = 8300):
# 列出分区表检查一下
Command (? for help): p
# 确认无误后写入，w 就是 write 的意思
Command (? for help): w
# 再三确认，小心丢失数据
Do you want to proceed? (Y/N): y

# 格式化引导分区，根分区和交换分区
$ mkfs.ext4 /dev/sda2
$ mkfs.ext4 /dev/sda4
$ mkswap /dev/sda3

# 挂载根分区
$ mount /dev/sda4 /mnt

# 创建用于挂载引导分区的文件夹
$ mkdir /mnt/boot

# 挂载引导分区
$ mount /dev/sda2 /mnt/boot

# 启动交换分区
swapon /dev/sda3
```

##### EFI 启动方式：

暂留

### 3. 安装：

只需要一行 `pacstrap /mnt base base-devel` 来进行安装，如果你觉得下载速度不行，尝试修改 `/etc/pacmand.d/mirrorlist` 来切换一个适合你的镜像源。

生成 **fstab**，`genfstab -U -p /mnt >> /mnt/etc/fstab`。特别注意这个只能生成一次，重复执行可就前功尽弃。

### 4. 配置系统：

```sh
# 首先切换到刚安装的环境
$ arch-chroot /mnt

# 修改语言，按个人习惯，去掉你想要语言前面的 #
$ vi /etc/locale.gen
# 我选择这个
en_US.UTF-8
# 加载一下刚才修改的
$ locale-gen

# 写入配置文件
echo LANG=en_US.UTF-8 > /etc/locale.conf

# 设置时间，因地区而异
$ ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

# 设置主机名，注意不是用户名
echo {你的主机名} > /etc/hostname

# 配置 hosts
$ vi /etc/hosts
# 在文件末尾加入
127.0.0.1 localhost {你刚才设置的主机名}

# 给 root 用户添加密码，不然等下登陆不了系统，输入密码的时候是不会显示出来的
passwd root
```

### 5. 配置引导：

这里我们又要把 `BIOS` 和 `EFI` 分开来说。

##### BIOS 启动方式：

```sh
# 安装 BIOS 启动方式的引导器
$ pacman -S grub-bios
$ grub-install --recheck /dev/sda
$ cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo
$ grub-mkconfig -o /boot/grub/grub.cfg

# 退出当前环境
exit

# 重启
reboot
```



##### EFI 启动方式：

暂留

### 6. 配置网络：

顺利的话经过上面的步骤重启后你会进入系统，但是没有网络。

```sh
# 查看网卡名
$ ls /sys/class/net/

# 启用网络连接
$ ip link set {上面找到的网卡名} up
# 例如我的是
$ ip link set enp0s5 up

# 动态获取 ip
$ dhcpcd {网卡名}

# 开机启动，以后每次开机就不用这样配置了
$ systemctl enable dhcpcd@{网卡名}

# 安装网络工具包
pacman -S net-tools

# 查看网络连接
ifconfig
```

### 7. 秀：

历尽千辛万苦终于装完，怎么能不秀个 logo？

```sh
$ pacman -S screenfetch

$ screenfetch
```
