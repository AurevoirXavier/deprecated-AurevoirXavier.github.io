---
layout: post
title: "OS X configure shadowsocks-libev with simple-obfs plugin"
date:   2018-7-10
excerpt: "OS X 下配置 shadowsocks-libev 配合 simple-obfs 插件"
tags: [shadowsocks, OS X]
comments: true
---

<center><h2>OS X 下配置 shadowsocks-libev 配合 simple-obfs 插件</h2></center>

<!--more-->

*最近这墙是越来越高了，运营商根据流量把你的代理给 QoS 了，所谓上有政策下有对策，得给 ***shadowsocks** 加个混淆才行*。

[ShadowsocksX-NG](https://github.com/shadowsocks/ShadowsocksX-NG) 虽然配置简单，但实在是不能随心所欲，所以我选择 [shadowsocks-libev](https://github.com/shadowsocks/shadowsocks-libev)。

#### With homebrew：

```sh
$ brew install shadowsocks-libve simple-obfs
$ vi /usr/local/etc/shadowsocks-libev.json
```

```json
{
    "server":"{服务器地址}",
    "server_port":{服务器端口},
    "local_port":{本地端口},
    "password":"{连接密码}",
    "timeout":300,
    "method":"{加密方式}",
    "plugin": "{这里特别注意，如果你要设置为服务随系统启动这里必须填写 obfs-local 的绝对路径，可以用 which obfs-local 找到，homebrew 安装的话就在 /usr/local/bin/obfs-local}",
    "plugin_opts": "obfs={服务器端混淆方式};obfs-host=www.bing.com"
} 
```

```sh
# 如果想要开机启动前面加上 sudo
$ brew service start shadowsocks-libev
```

#### With nix:

最近发现 [nix](https://nixos.org/nix/) 这个包管理器的设计理念非常不错，于是乎打算放弃 homebrew。

比如说，编译 librsvg 需要 rust，rust 需要 llvm ，llvm 有一个选项需要 graphviz，graphviz 需要 librsvg，这时候 homebrew 一点办法都没有了，而 nix 选择从源码先编译一次没有 graphviz 选项的 llvm 再完成所有工作。

又或者说，homebrew 每次升级 python 带来的一大堆连接丢失问题，然而 nix 可以[这样](https://www.slideshare.net/datakurre/nix-for-python-developers)。

回到正题来谈谈用 nix 安装，并搭配 [launchctl](http://www.launchd.info) 配置开机启动，还可以省去写一个 json 配置文件：

```sh
$ nix-env -iA nixpkgs.shadowsocks-libev
$ vi ~/Library/LaunchAgents/com.github.shadowsocks.plist
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
	<dict>
        <key>Label</key>
        <string>com.github.shadowsocks.plist</string>

        <key>ProgramArguments</key>
        <array>
			<string>/Users/{你的用户名}/.nix-profile/bin/ss-local</string>
			<string>-s</string>
			<string>{服务器地址}</string>
			<string>-p</string>
			<string>{服务器端口}</string>
			<string>-l</string>
			<string>{本地端口}</string>
			<string>-k</string>
			<string>{连接密码}</string>
			<string>-m</string>
			<string>{加密方式}</string>
			<string>--plugin</string>
			<string>{这里特别注意，如果你要设置为服务随系统启动这里必须填写 obfs-local 的绝对路径，可以用 which obfs-local 找到，homebrew 安装的话就在 /usr/local/bin/obfs-local}</string>
			<string>--plugin-opts</string>
			<string>obfs={服务器端混淆方式};obfs-host=www.bing.com</string>
		</array>

		<key>KeepAlive</key>
		<true/>

		<key>RunAtLoad</key>
		<true/>
	</dict>
</plist>
```

```sh
$ launchctl load ~/Library/LaunchAgents/com.github.shadowsocks.plist
```

#### 启用代理

光启用服务了还不行，还要：

1.  -> System Preferences…（系统偏好） -> Network（网络）-> Advanced…（高级）-> Proxies（代理）
2. SOCKS Proxy（SOCKS 代理）打上勾
3. SOCKS Proxy Server（代理服务器）服务器地址填入 `127.0.0.1` 端口填入上面设置的 `{本地端口}`
4. 关于 Automatic Proxy Configuration（自动代理配置），各有喜好，我选择白名单模式的 pac 只要不在名单内的均启用代理，当然流量比较少的人可以选用黑名单模式的。如果不启用的话，所有网站都走代理，那么国内网站访问就很慢啦。

最后附上著名的黑名单 pac [gfwlist](https://github.com/gfwlist/gfwlist)，以及白名单 pac [gfw_whitelist](https://github.com/breakwa11/gfw_whitelist)。