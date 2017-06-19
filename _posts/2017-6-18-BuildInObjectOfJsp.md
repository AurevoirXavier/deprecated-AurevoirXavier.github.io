---
layout: post
title: "Jsp's build-in object"
date:   2017-06-18
excerpt: "Servlet 与九大内置对象"
tags: [jsp, program]
comments: true
---



|   Jsp 对象    |          如何获得          |
| :---------: | :--------------------: |
|     out     |     resp.getWriter     |
|   request   |  service 方法中的 req 参数   |
|  response   |  service 方法中的 resp 参数  |
|   session   |  req.getSession() 函数   |
| application | getServletContext() 函数 |
|  exception  |       Throwable        |
|    page     |          this          |
| pageContext |      PageContext       |
|   Config    |  getServletConfig 函数   |

