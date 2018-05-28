---
layout: post
title: "shadowsocks server deploy"
date:   2017-10-25
excerpt: "shadowsocks 服务器搭建"
tags: [shadowsocks]
comments: true
---

<center><h2>shadowsocks 服务器搭建</h2></center>

<!--more-->

### 服务器选择：

个人推荐 [vultr](https://www.vultr.com/?ref=7243921)，在我这里是能达到百兆光纤速度的上限。

<a href="https://www.vultr.com/?ref=7243921"><img src="https://www.vultr.com/media/banner_1.png" width="728" height="90"></a>

### 创建用户：

这个没什么好说的吧。

### Server Location 地区:

看个人需求了，一般来说是机房地理位置离你越近越好。我选择的是 `Tokyo Japan` 的机房。

### Server Type & Server Size 服务器配置：

- 操作系统：Debian 7 x64
- 硬盘空间：25GB SSD
- 处理器：1 CPU
- 内存：1024MB
- 可用流量：1000GB

以上是推荐个人或者两个人共同使用的配置，如有特别需求自行选择。

### Additional Features 附加功能：

- IPv6 `启用 IPv6`：✗
- Private Network `私有网络`：✗
- AutoBackups `自动备份`：✓
- DDos Protection `DDos 保护`：✗
- Block Storage Compatible `储存区块`：✗

**Tips：**

1. 私有网络其实就是添加内网地址。
2. 自动备份（这里我开启了没什么用处的话不推荐你们开启）。
3. DDos 保护就是防御洪水攻击的，如果你只是为了翻墙一般是没用的。
4. 免费提供的储存区块对于我们翻墙来说没什么用。不过这个功能仅限纽约和新泽西的服务器可以使用。

### Startup Script 启动脚本：

开机时会自动执行的脚本，不过我不在此设置。

### SSH Keys：

和自己执行 `ssh-copy-id` 实现免密登陆有异曲同工之妙。不过需要的注意的是点击 Add Keys 并且把公钥保存之后，需要回到部署页面刷新一下然后才会出现刚添加的项目，然后单击底色变蓝说明勾选。

### Server Hostname & Label 域名与标签：

如果你有域名可以绑上去，远程连接或者使用 shadowsocks 的时候就不用记那一串 ip 地址了。

---

### 连接服务器：

使用 `putty` 或者 `ssh`，或者直接使用部署成功后进入服务器网页里面的 `console`。网上过多教程，此处不在赘述。

---

### 安装 shadowsocks：

一键脚本（由 teddysun 提供）：

```sh
wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-libev-debian.sh && chmod +x shadowsocks-libev-debian.sh && ./shadowsocks-libev-debian.sh 2>&1 | tee shadowsocks-libev-debian.log
```

安装过程中会遇到几次要求输入的地方：

1. 输入密码，密码就是要求你输入的地方前面那个括号里，我记得应该是 `teddysun.com`。
2. 使用端口，输入 `443`。
3. 加密方式：`rc4-md5`，输入前面的序号，我记得应该是 `18` 。

### 安装 BBR（可选）：

最近，Google 开源了其 TCP BBR 拥塞控制算法，并提交到了 Linux 内核，从 4.9 开始，Linux 内核已经用上了该算法。根据以往的传统，Google 总是先在自家的生产环境上线运用后，才会将代码开源，此次也不例外。
根据实地测试，在部署了最新版内核并开启了 TCP BBR 的机器上，网速甚至可以提升好几个数量级。
一键脚本（由 teddysun 提供）：

```sh
wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh && chmod +x bbr.sh && ./bbr.sh
```

安装完成后，脚本会提示需要重启 VPS，输入 y 并回车后重启。
重启完成后，进入 VPS，验证一下是否成功安装最新内核并开启 TCP BBR，输入以下命令：

```sh
uname -r
```

查看内核版本，含有 4.13 就表示 OK 了

```sh
sysctl net.ipv4.tcp_available_congestion_control
```

返回值一般为：
`net.ipv4.tcp_available_congestion_control = bbr cubic reno`

```sh
sysctl net.ipv4.tcp_congestion_control
```

返回值一般为：
`net.ipv4.tcp_congestion_control = bbr`

```sh
sysctl net.core.default_qdisc
```

返回值一般为：
`net.core.default_qdisc = fq`

```sh
lsmod | grep bbr
```

返回值有 tcp_bbr 模块即说明 bbr 已启动。注意：并不是所有的 VPS 都会有此返回值，若没有也属正常。

**内核升级方法**

如果是 CentOS 系统，执行如下命令即可升级内核：

```sh
yum --enablerepo=elrepo-kernel -y install kernel-ml kernel-ml-devel
```

CentOS 6 的话，执行命令：

```sh
sed -i 's/^default=.*/default=0/g' /boot/grub/grub.conf
```

CentOS 7 的话，执行命令：

```sh
grub2-set-default 0
```

如果是 Debian/Ubuntu 系统，则需要手动下载最新版内核来安装升级。
去[这里](http://kernel.ubuntu.com/~kernel-ppa/mainline/)下载最新版的内核 deb 安装包。
如果系统是 64 位，则下载 amd64 的 linux-image 中含有 generic 这个 deb 包；
如果系统是 32 位，则下载 i386 的 linux-image 中含有 generic 这个 deb 包；
安装的命令如下（以最新版的 64 位 4.12.4 举例而已，请替换为下载好的 deb 包）：

```sh
dpkg -i linux-image-4.12.4-041204-generic_4.12.4-041204.201707271932_amd64.deb
```

安装完成后，再执行命令：

```sh
/usr/sbin/update-grub
```

重启即可。

**特别说明**

如果你使用的是 Google Cloud Platform （GCP）更换内核，有时会遇到重启后，整个磁盘变为只读的情况。只需执行以下命令即可恢复：

```sh
mount -o remount rw /
```

### 安装锐速 （可选）：

锐速起到一个加速的作用，其实就像是马路上的红绿灯，用算法调节阻塞。

一键脚本（由 teddysun 提供）：

```shell
wget -N --no-check-certificate https://raw.githubusercontent.com/91yun/serverspeeder/master/serverspeeder-all.sh && bash serverspeeder-all.sh
```

如果想删除锐速：

```shell
chattr -i /serverspeeder/etc/apx* && /serverspeeder/bin/serverSpeeder.sh uninstall -f
```

**锐速开机自启：**

编辑 `/etc/rc.local`。

rc.local：

```shell
service serverSpeeder start
```

------

### 最后配置：

编辑 `/etc/shadowsocks-libev/config.json` ，至于选择什么编辑器自行百度一下，毕竟看这个教程的大部分是新手而 linux 的许多编辑器对新手确实是不太友好例如 vi。

config.json ：

```json
"server":"0.0.0.0",
"server_port":这里是你 ss 服务器开放的端口用之前配置好的 443 就好了,
"local_address":"127.0.0.1",
"local_port":1080,
"password":"这里填写用来连接你 ss 的密码",
"timeout":600,
"method":"这里是加密方式同样用之前配置好的 rc4-md5 就行了"
```

### 防火墙（可选）：

安装防火墙：

```shell
apt-get install firewalld
```

放行 443 端口：

```shell
firewall-cmd --permanent --zone=public --add-port=443/tcp
```

重新加载放行列表：

```shell
firewall-cmd --reload
```

---

### 至此，世界地图上又重新出现了中国。