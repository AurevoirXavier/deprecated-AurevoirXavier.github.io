---
layout: post
title: "Include in Jsp"
date:   2017-06-18
excerpt: "Jsp 中的 include"
tags: [program, web]
comments: true
---

|              |        include 指令        |      Jsp:include 动作       |
| :----------: | :----------------------: | :-----------------------: |
|     语法格式     | <%@ include file = "" %> | \<jsp:include page = "" > |
|   发生作用的时间    |          页面转换期间          |           请求期间            |
|    包含的内容     |         文件的实际内容          |           页面的输出           |
| 转换成的 Servlet |  主页面和包含页面转换为一个 Servlet   |  主页面和包含页面转换为独立的 Servlet   |
|     编译时间     |      较慢 - 资源比必须被解析       |            较快             |
|     执行时间     |            稍快            |      较慢 - 每次资源必须被解析       |

