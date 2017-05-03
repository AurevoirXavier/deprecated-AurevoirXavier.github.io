---
layout: post
title: "setProperty in Jsp"
date:   2017-05-3
excerpt: "Jsp 中的 setProperty"
tags: [java, jsp, program]
comments: true
---

## \<jsp:setProperty> 是用来给已经实例化的 JavaBean 对象的属性赋值。那么该如何使用 \<jsp:setProperty>？

*方法一：*

`<jsp:setProperty name = "JavaBean 实例名" property = "*"/>` 此方法跟 **form** 关联

*方法二：*

`<jsp:setProperty name = "JavaBean 实例名" property = "JavaBean 属性名"/>` 此方法跟 **form** 关联

*方法三：*

`<jsp:setProperty name = "JavaBean 实例名" property = "JavaBean 属性名" value = "JavaBean 对应属性名的值"/>` 此方法为纯手工设置

*方法四：*

`<jsp:setProperty name = "JavaBean 实例名" property = "JavaBean 属性名" param = "request 对象中的参数名"/>` 此方法跟 **request** 参数关联

## 以下源码可供你体验四种方式，去掉方法体注释即可看到效果：

<center><strong>User.java</strong></center>

```java
package com.po;

public class User {
    private String name;
    private String id;

    public User() {}

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }
}
```

<center><strong>index.jsp</strong></center>

```html
<%@ page import="com.po.User" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Ex1</title>
</head>
<body>
<form name="loginForm" action="deal.jsp?param=6" method="post">
    <table align="center">
        <tr>
            <td>Username:</td>
            <td><input type="text" name="name" placeholder="username"></td>
        </tr>
        <tr>
            <td>Id:</td>
            <td><input type="text" name="id" placeholder="id"></td>
        </tr>
        <tr>
            <td colspan="2" align="center"><input type="submit" value="Login"/></td>
        </tr>
    </table>
</form>
</body>
</html>
```

<center><strong>deal.jsp</strong></center>

```html
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Ex2</title>
</head>
<body>
<jsp:useBean id="myUser" class="com.po.User" scope="page"/>
<h1>setProperty</h1>
<hr>
<%--方法一：根据 form 自动匹配所有属性。对应原则：java 文件中的私有变量名对应此处的 property，* 代表全部匹配。--%>
<%--<jsp:setProperty name="myUser" property="*"/>--%>
<%--方法二：大致如方法一，但由自己手动匹配属性。--%>
<%--<jsp:setProperty name="myUser" property="id"/>--%>
<%--方法三：与 form 无关，手动赋值。注意：方法二是手动匹配，此处是手动赋值。value 参数处可以用 request 赋值，但是那样就是自己找不自在了，不如选用前两种方法。--%>
<%--<jsp:setProperty name="myUser" property="name" value="Mr.A"/>--%>
<%--<jsp:setProperty name="myUser" property="id" value="1"/>--%>
<%--方法四：与 request 提交的参数有关，不一定使用表单参数可以用 URL 传来的参数。--%>
<jsp:setProperty name="myUser" property="id" param="param"/>
<%--=================================================================================================--%>
Username: <%=myUser.getName()%>
<br>
Id: <%=myUser.getId()%>
<br>
</body>
</html>
```

