---
layout: post
title: "Token vs. Session"
date:   2017-05-4
excerpt: "Web 应用中的 Token 与 Session"
tags: [json, program, web]
comments: true
---

许多现代 *Web 应用程序* 使用 **JSON Web Tokens (JWT)**，而不是传统的基于 **session** 的*身份验证*。在现代应用程序中使用服务器端会话已经发现了很多挑战。在这篇文章中，我们将确定这些挑战，并解释 **JWT** 和 **sessions** 在实践中如何工作。

<code class="highlighter-rouge">最近有关于 <strong>JWT</stong> 真正发光的用例以及那些做得不好的工作的争议。也就是说，<strong>JSON Web Tokens</strong> 对于 <strong>sessions</strong> 来说足够好 - 还是应该继续使用 <strong>cookies</strong>？</code>

## 什么是 JSON Web Tokens?

**JSON Web Token (JWT)** 是一种开放标准 ([RFC 7519](https://tools.ietf.org/html/rfc7519))，它定义了一种紧凑且 *self-contains (自包含)* 的方式，可以作为 **JSON** 对象在各方之间安全地传输信息。该信息可以通过*数字签名*进行*验证*和*信任*。**JWTs** 可以使用密钥 (使用 *HMAC 算法*) 或使用 *RSA 的公钥/私钥*对进行*签名*。

## 剖析 JWT

**JWTs** 基本上由三部分组成由一个 `.` 分隔。*header (标头)*，*payload (有效载荷)* 和*签名*。接下来将对 *JWT 结构* 进行全面的解释。查看这篇优秀[文章](https://auth0.com/learn/json-web-tokens/)，有着对 *JWT 结构*的全面解释。

## JSON Web Tokens 的工作原理

在*身份验证*中，当用户使用其凭据成功登录时，将返回一个 **JSON Web Token**，并且必须保存在本地 (通常在本地存储中，但也可以使用 **cookies**)，而不是像传统的方法一样，在服务器中创建一个会话并返回一个 **cookie**。

每当用户想要访问受保护的路由时，它应该发送 **JWT**，通常在*授权*头中使用承载模式。因此，标题的内容应如下：

```json
Authorization: Bearer <token>
```

这是一种 *stateless (无状态的) 认证机制*，因为用户状态永远不会保存在服务器内存中。服务器的受保护路由将在*授权标头*中检查有效的 **JWT**，如果存在，那么用户将被允许。由于 **JWTs** 是独立的，所有必要的信息都在那里，从而减少了对数据库的需求。

这允许用户完全依赖*无状态的*数据 *APIs*，甚至向下游服务发出请求。由于不使用 **cookies**，因此，*Cross-Origin Resource Sharing (CORS (跨原始资源共享))* 不会成为问题，因此无论哪个域用于你的 *APIs* 都不重要。

**认证流程**

![](http://imgur.com/VBQMuz9.png)

## 为什么应该使用 JWTs？

你应该使用 **JSON Web Tokens** 以下几个原因：

- 它们易于水平缩放
- 它们更容易维护和调试
- 他们有能力创建真正的 **RESTful** 服务
- 它们具有内置的到期功能
- **JSON Web Tokens** 是独立的

上面的要点将在下面详细解释。

## JWTs vs. Sessions

在出现 **JSON Web Tokens** 之前，主要采用基于服务器的*身份验证*。众所周知，*HTTP 协议*是*无状态的*，这意味着如果使用用户名和密码验证用户，那么在下一个*请求*中，应用程序将不知道是谁。必须再次验证。因此，需要确保在用户登录后，仍然可以在每个后续 *HTTP 请求*中*验证用户的身份验证状态*。

![](http://imgur.com/zlI226h.png)

用户的凭据作为 *POST 请求* 发送到服务器。服务器*认证*用户。如果凭据有效，则服务器将使用 **cookie** 进行响应，该 **cookie** 是在用户浏览器上设置的，并包含一个 **SESSION ID** 以标识该用户。用户会话通过文件或服务器上的数据库存储在内存中。在本节中，将详细阐述几点，这些要点将作为在实践中比较 **JWTs** 与 **sessions** 的基础。

**1.可扩展性：**随着应用程序的增长和用户数量的增加，你必须开始水平或垂直缩放。会话数据通过文件或数据库存储在服务器的内存中。在水平扩展方案中，你必须开始复制服务器，你必须提出一个单独的中央会话存储系统，以便所有应用程序服务器都可以访问。否则，由于会话存储的缺陷，你将无法扩展应用程序。解决这个挑战的另一种方法是使用 [*sticky sessions* (粘性会话)](http://stackoverflow.com/questions/10494431/sticky-and-non-sticky-sessions) 的概念。你还可以将 **sessions** 存储在磁盘上，使你的应用程序在云环境中轻松扩展。这些类型的解决方法在现代大型应用中并没有真正发挥。建立和维护这种分布式系统涉及到深入的技术知识，并随之产生更高的财务成本。在这种情况下，使用 **JWTs** 是无缝的;由于基于 **token** 的*身份验证*是*无状态的*，所以不需要在 **session** 中存储用户信息。应用程序可以轻松扩展，因为可以使用 **tokens** 从不同的服务器访问资源，而不用担心用户是否实际登录到特定的服务器上。你也可以节省成本，因为你不需要专门的服务器来存储 **sessions**。为什么？因为根本没有 **sessions**！

**注意：**如果你正在构建不需要扩展到在多台服务器上运行且不需要 *RESTful API* 的小型应用程序，那么 **sessions** 足以胜任。如果你有专用的服务器用于运行 *Redis* 这样的工具来 **sessions** 存储，那么 **sesions** 也会完美工作！

**2.安全性：**签署 **JWTs** 旨在防止客户端的篡改，但也可以对其进行加密，以确保 **token** 携带的声明非常安全。现在，**JWTs** 主要是直接存储在网络存储 *(local/session storage)* 或 **cookies** 中。*JavaScript* 可以访问同一个域上的 *Web存储*。这仅仅意味着你的 **JWTs** 可能容易受到 *XSS (Cross-site Scripting)* 攻击。可以将恶意 *JavaScript* 嵌入在页面上，以读取和损害 *Web存储*的内容。由于 *XSS 攻击*，事实上，很多人主张，非常敏感的数据不应该存储在 *Web存储*中。一个非常典型的例子是确保你的 **JWTs** 不被非常敏感/可信任的数据编码，例如用户的社会安全号码。

最初，我提到 **JWTs** 可以存储在 **cookies** 中。 事实上，**JWTs** 在许多情况下被存储为 **cookies**，并且 **cookies** 很容易受到 [*CSRF (Cross-site Request Forgery)*](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) 攻击的影响。预防 *CSRF* 攻击的许多方法之一是确保你的 **cookies** 只能由你的域访问。作为开发人员，不管使用 **JWTs**，确保必要的 *CSRF* 保护措施到位以避免这些攻击。

现在，**JWTs** 和 **session ids** 也可以暴露到 *reply 攻击*。完全由开发者确定哪些 *reply-mitigation* 技术适合于他们的系统。解决这个问题的一个方法是确保 **JWTs** 依靠短期到期。虽然这种技术并不能完全解决问题。然而，解决这个挑战的其他替代方案是将 **JWTs** 发布到特定的 *IP* 地址并使用 [*borwser fingerprinting* (浏览器指纹)](http://www.networkworld.com/article/2884026/security0/browser-fingerprints-and-why-they-are-so-hard-to-erase.html)。

**注意：**使用 *HTTPS/SSL* 确保你的 **cookies** 和 **JWTs** 在客户端和服务器传输期间默认加密。这有助于避免 *man-in-the-middle (中间人)* 的攻击！

**3.RESTful API 服务：**现代应用程序的常见模式是从 *RESTful API* 检索和使用 *JSON* 数据。目前大多数应用程序都有 [*RESTful API*](http://www.restapitutorial.com/) 供其他开发人员或应用程序使用。从 *API* 提供的数据具有几个明显的优点，其中之一就是在不只一个应用程序中使用数据的能力。 在这种情况下，传统的使用 **sessions**和 **cookies** 的方法在用户身份方面效果不佳，因为它们向应用程序引入了 *state (状态)*。

*RESTful API* 的一个原理是它应该是*无状态的*，这意味着当发出*请求*时，在某些参数中的响应总是可以预期的，没有副作用。用户的 *authentication state (认证状态)* 引入了这种副作用，这破坏了这一原则。保持 *API* 无状态，因此没有副作用意味着可维护性和调试变得更加容易。

这里的另一个挑战是，从一个服务器提供 **API**，并且实际应用程序从另一个服务器使用 *API* 是很常见的。为了实现这一点，我们需要启用 *[Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS)* (跨原始资源共享)。由于 **cookies** 只能用于其发起的域，因此对于不同于应用的域的 *APIs* 来说，它们不是很有帮助。在这种情况下使用 **JWTs** 进行*身份验证*可以确保 *RESTful API 无状态的*，也不用担心 *API* 或应用程序从何处来。

**4.性能：**对此的批判性分析是非常必要的。当从客户端向服务器发出*请求*时，如果大量数据在 **JWT** 内进行编码，则每个 *HTTP请求* 都会产生大量的开销。然而，在 **sessions** 中，只有少量的开销，因为 **SESSION IDs** 实际上非常小。看下面这个例子：

一个有 5 个宣称的 **JWT**：

```json
{
  "sub": "1234567890",
  "name": "Aurevoir Xavier",
  "admin": true,
  "role": "manager",
  "company": "Auth0"
}
```

编码时，**JWT** 的大小将是 **SESSION ID** *(identifier (标识符))* 大小的几倍，从而使每个 *HTTP请求* 都使得该 **JWT** 比 **SESSION ID** 增加更多的开销。对于 **sessions**，还有一个服务器端查找可以查找和 *deserialize (反序列化)* **sessions** 的每一个*请求*。

**JWTs** 通过将数据保留在客户端来交换大小的延迟。你的应用程序的数据模型是一个重要的因素，因为通过防止对服务器上的数据库进行不间断的调用和查询来保存延迟。这里的想法是要谨慎，不要在 **JWT** 中存储太多的索赔，以避免发生巨大的，过度膨胀的*请求*。

值得一提的是，**tokens** 可能需要访问后端的数据库。特别是刷新 **tokens** 的情况。他们可能需要访问*授权服务器*上的数据库以进行黑名单。获取有关[刷新 **tokens** 和何时使用它们](https://auth0.com/blog/refresh-tokens-what-are-they-and-when-to-use-them/)的更多信息。另外，请查看这篇[文章](https://auth0.com/blog/blacklist-json-web-token-api-keys)，了解有关黑名单的更多信息。

**注意：**开发者需学会衡量何时应该使用 **JWTs**！

![](http://imgur.com/GSjpyju.jpg)

**5.下游服务：** 现代 *Web 应用程序*看到的另一种常见模式是它们常常依赖于下游服务。例如，在解决*原始请求*之前，对主应用程序服务器的调用可能会向下游服务器发出请求。这里的问题是，**cookies** 不会轻易地流向下游的服务器，也不能告诉这些服务器有关用户的*身份验证状态*。由于每个服务器都有自己的 **cookies** 方案，因此流量很大，连接困难。**JSON Web Tokens** 再次使这些变得轻而易举！

## 使用 JWTs 验证 Auth0

在 *Auth0* 中，由于*认证*过程，发布了 **JWTs**。当用户使用 *Auth0* 登录时，创建，*签名*并发送给用户的 **JWT**。*Auth0* 支持使用 *HMAC 和 RSA 算法*来*签名***JWT**。用户可以灵活地从仪表板中实际选择这两种算法。然后，该 **token** 将用于使用 *APIs* 进行*身份验证*和*授权*，这将允许访问其受保护的路由和资源。

还使用 **JWTs** 在 [*Auth0 的 API v2*](https://auth0.com/docs/api/management/v2) 中执行*认证*和*授权*，取代了常规不透明 *API* 密钥的传统用法。关于*授权*，**JSON Web Tokens** 允许精细的安全性，这是能够在 **token** 中指定一组特定权限，从而提高可调试性。

## 结论

**JSON Web Token** 是轻量级的，可以轻松地跨平台和语言使用。是一个聪明的方式来*验证*和*授权*没有 **sessions**。有几个 *JWT 库*可用于*签名*和*验证* **tokens**。使用 **tokens** 的原因还有很多，*Auth0* 可以通过简单，安全的方式实现 **token** *认证*。

就个人而言，我认为没有一个一刀切的方法。它将始终取决于你的应用程序架构和用例。

你仍然更喜欢在实践中使用 *JSON Web代码*？让我们在评论部分知道你的想法！