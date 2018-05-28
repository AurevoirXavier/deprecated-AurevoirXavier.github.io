---
layout: post
title: "Tomcat directory structure"
date:   2017-04-27
excerpt: "Tomcat 目录结构"
tags: [Tomcat, Web]
comments: true
---

<center><h2>Tomcat 服务器的目录结构</h2></center>

<!--more-->

| <font color="red">目录</font>       | <font color="blue">说明</font>    |
| :------- | :--------------------------------------- |
| /bin     | 存放各种平台下启动和停止 **Tomcat** 的命令文件，如 **startup.sh**，**startup.bat** |
| /conf    | 存放 **Tomcat** 的各种配置文件                    |
| /lib     | 存放 **Tomcat** 服务器所需的各种 JAR 文件            |
| /log     | 存放 **Tomcat** 的日志文件                      |
| /temp    | **Tomcat** 运行时用于存放临时文件                   |
| /webapps | 当发布 **Web** 应用时，默认会将 **Web** 应用的文件发布到此目录中 |
| /work    | **Tomcat** 把由 **Jsp** 生成的 **Servlet** 放在此目录下 |