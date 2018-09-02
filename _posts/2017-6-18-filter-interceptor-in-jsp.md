---
layout: post
title: "filter and interceptor in Jsp"
date:   2017-06-18
excerpt: "Jsp 中的过滤器与拦截器"
tags: [Java]
comments: true
---

|        filter (过滤器)         |  interceptor (拦截器)   |
| :-------------------------: | :------------------: |
| 依赖于 Servlet 容器，基于回调函数，过滤范围大 | 依赖于框架容器，基于反射机制，只过滤请求 |

多个拦截器如何工作呢？

![多拦截器协同工作流程图](https://i.imgur.com/sFLnShN.png)