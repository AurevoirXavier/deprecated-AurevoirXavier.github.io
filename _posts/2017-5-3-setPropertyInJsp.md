---
layout: post
title: "setProperty in Jsp"
date:   2017-05-3
excerpt: "Java 中的 setProperty"
tags: [java, jsp, program]
comments: true
---

**\<jsp:setProperty> 是用来给已经实例化的 JavaBean 对象的属性赋值。**

**那么该如何使用 \<jsp:setProperty>？**

*方法一：*

`<jsp:setProperty name = "JavaBean 实例名" property = "*"/>` 此方法跟 **form** 关联

*方法二：*

`<jsp:setProperty name = "JavaBean 实例名" property = "JavaBean 属性名"/>` 此方法跟 **form** 关联

*方法三：*

`<jsp:setProperty name = "JavaBean 实例名" property = "JavaBean 属性名" value = "JavaBean 对应属性名的值"/>` 此方法为纯手工设置

*方法四：*

`<jsp:setProperty name = "JavaBean 实例名" property = "JavaBean 属性名" param = "request 对象中的参数名"/>` 此方法跟 **request** 参数关联