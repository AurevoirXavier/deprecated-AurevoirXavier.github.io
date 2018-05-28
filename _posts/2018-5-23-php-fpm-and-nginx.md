---
layout: post
title: "Configure php-fpm and nginx"
date:   2018-05-23
excerpt: "php-fpm 与 nginx"
tags: [php, nginx]
comments: true
---

<center><h2>php-fpm 与 nginx</h2></center>

<!--more-->

一开始 *nginx* 老是报 **502**，然后使用 `netstat -anp | grep 9000` 后，发现 **9000** 端口没有程序。起初以为是没有启动成功。后来运行 `systemctl status php7.0-fpm.service` 发现运行正常。这时候就想到应该是配置出了问题。

`vi /etc/php/7.0/fpm/php-fpm.conf` 后发现，原来是默认监听的内容变了。默认监听内容为 `listen = /var/run/php/php7.0-fpm-domain1.sock`。

那么有两种办法：

1. 修改 *nginx* 对应监听地址为 `/var/run/php/php7.0-fpm-domain1.sock`。
2. 修改 *php-fpm* 对应监听地址为 `127.0.0.1:9000`。

总之两者统一就可以了。