---
layout: post
title: "setProperty in Jsp"
date:   2017-05-3
excerpt: "Java 中的 setProperty"
tags: [java, jsp, program]
comments: true
---

# \<jsp:setProperty> 有什么用？

它是用来给已经实例化的 JavaBean 对象的属性赋值。

# 怎样使用 \<jsp:setProperty>？

一共有四种使用方法，下面将一一讲解。

## 方法一：

`\<jsp:setProperty name = "JavaBean 实例名" property = "*"/>`

## 方法二：

`\<jsp:setProperty name = "JavaBean 实例名" property = "JavaBean 属性名"/>`

## 方法三：

`\<jsp:setProperty name = "JavaBean 实例名" property = "JavaBean 属性名" value = "JavaBean 对应属性名的值"/>`

## 方法四：

`\<jsp:setProperty name = "JavaBean 实例名" property = "JavaBean 属性名" param = "request 对象中的参数名"/>`