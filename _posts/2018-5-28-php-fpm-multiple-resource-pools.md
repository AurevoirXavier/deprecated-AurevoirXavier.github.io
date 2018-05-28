---
layout: post
title: "PHP-FPM: Multiple Resource Pools"
date:   2018-05-28
excerpt: "PHP-FPM: 多资源池"
tags: [php]
comments: true
---

<center><h2>PHP-FPM: 多资源池</h2></center>

<!--more-->

```sh
# 首先安装必备组件
sudo apt-get install -y nginx php-fpm php-cli php-curl php-mcrypt php-mysql php-gd

# 复制多一分配置文件，一份配置文件对应一个服务
sudo cp /etc/php7/fpm/pool.d/www.conf /etc/php7/fpm/pool.d/new.conf

vi /etc/php7/fpm/pool.d/new.conf
# 修改 www 为新配置文件的名字即 new
[new]

# 修改监听配置，使每个配置文件的端口或进程必须为独立唯一的
listen = /var/run/php5-fpm-app.sock;
listen = 127.0.0.1:9001;
```