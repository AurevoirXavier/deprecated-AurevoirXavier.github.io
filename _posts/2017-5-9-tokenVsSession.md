---
layout: post
title: "Token Vs. Session"
date:   2017-05-4
excerpt: "Web 应用中的 Token 与 Session"
tags: [json, program, web]
comments: true
---

许多现代 **Web 应用程序** 使用 **JSON Web Tokens (JWT)**，而不是传统的基于 **session** 的身份验证。在现代应用程序中使用服务器端会话已经发现了很多挑战。在这篇文章中，我们将确定这些挑战，并解释 **JWT** 和 **sessions** 在实践中如何工作。

<code class="highlighter-rouge">最近有关于 <strong>JWT</stong> 真正发光的用例以及那些做得不好的工作的争议。也就是说，<strong>JSON Web Tokens</strong> 对于 <strong>sessions</strong> 来说足够好 - 还是应该继续使用 <strong>cookies</strong>？</code>

## 什么是 JSON Web Tokens?

**JSON Web Token (JWT)** 是一种开放标准 ([RFC 7519](https://tools.ietf.org/html/rfc7519))，它定义了一种紧凑且自包含的方式，可以作为 **JSON** 对象在各方之间安全地传输信息。该信息可以通过数字签名进行验证和信任。**JWT** 可以使用秘密 (使用 **HMAC** 算法) 或使用 **RSA** 的公钥/私钥对进行签名。

## 剖析 JWT

**JWTs** 基本上由三部分组成由一个 `.` 分隔。标题，有效载荷和签名。接下来将对 **JWT 结构** 进行全面的解释。

## JSON Web Tokens 的工作原理

在身份验证中，当用户使用其凭据成功登录时，将返回一个 **JSON Web Token**，并且必须保存在本地 (通常在本地存储中，但也可以使用 **cookies**)，而不是像传统的方法一样，在服务器中创建一个会话并返回一个 **cookie**。

每当用户想要访问受保护的路由时，它应该发送 **JWT**，通常在授权头中使用承载模式。因此，标题的内容应如下：

```json
Authorization: Bearer <token>
```

这是一种无状态认证机制，因为用户状态永远不会保存在服务器内存中。服务器的受保护路由将在授权标头中检查有效的 **JWT**，如果存在，那么用户将被允许。由于 **JWT** 是独立的，所有必要的信息都在那里，从而减少了对数据库的需求。

这允许用户完全依赖无状态的数据 APIs，甚至向下游服务发出请求。由于不使用 cookies，因此，跨原始资源共享 **(CORS)** 不会成为问题，因此无论哪个域用于你的 APIs 都不重要。

**认证流程**

![](http://imgur.com/VBQMuz9.png)

## 为什么应该使用 JWT？

你应该使用 **JSON Web Tokens** 以下几个原因：

- 它们易于水平缩放
- 它们更容易维护和调试
- 他们有能力创建真正的 **RESTful** 服务
- 它们具有内置的到期功能
- **JSON Web Tokens** 是独立的

上面的要点将在下面详细解释。

