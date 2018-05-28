---
layout: post
title: "build-in object of Jsp"
date:   2017-06-18
excerpt: "Jsp 内置对象"
tags: [Java, Web]
comments: true
---

<center><h2>Jsp 内置对象</h2></center>

<!--more-->

<center>
|||
| :---------: | :--------------------: |
|   <font color="red">Clarifai</font>    |    <font color="blue">如何获得</font>    |
|     out     |     resp.getWriter     |
|   request   |  service 方法中的 req 参数   |
|  response   |  service 方法中的 resp 参数  |
|   session   |  req.getSession() 函数   |
| application | getServletContext() 函数 |
|  exception  |       Throwable        |
|    page     |          this          |
| pageContext |      PageContext       |
|   Config    |  getServletConfig 函数   |
</center>