---
layout: post
title: "Enable php pathinfo with nginx"
date:   2018-05-23
excerpt: "配置 nginx 启用 php pathinfo"
tags: [php, nginx]
comments: true
---

<center><h2>配置 nginx 启用 php pathinfo</h2></center>

<!--more-->

`sudo vi /usr/local/nginx/conf/enable-php-pathinfo.conf`:

```sh
 location ~ [^/]\.php(/|$) {
    #listen unix socket
    #fastcgi_pass  unix:/tmp/php-cgi.sock;
    #listen tcp socket
    fastcgi_pass  127.0.0.1:9000;

    fastcgi_index index.php;
    include fastcgi.conf;

    #pathinfo
    fastcgi_split_path_info ^(.+?\.php)(/.*)$;
    set $path_info $fastcgi_path_info;
    fastcgi_param PATH_INFO $path_info;
    try_files $fastcgi_script_name =404;
}
```