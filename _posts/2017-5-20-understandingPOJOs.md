---
layout: post
title: "Understanding POJOs"
date:   2017-05-20
excerpt: "理解 POJOs"
tags: [springmvc, translate]
comments: true
---

POJO 表示 **Plain Old Java Object** (普通 Java 对象)。它是指 Java 对象 (定义的实例)，不被框架扩展所阻碍。

例如，要从 JMS 接收消息，你需要编写一个实现 `MessageListener` 接口的类。

```java
public class ExampleListener implements MessageListener {

    public void onMessage(Message message) {
        if (message instanceof TextMessage) {
            try {
                System.out.println(((TextMessage) message).getText());
            }
            catch (JMSException ex) {
                throw new RuntimeException(ex);
            }
        }
        else {
            throw new IllegalArgumentException("Message must be of type TextMessage");
        }
    }

}
```


这将你的代码与特定解决方案 (此示例中为 JMS) 相结合，并使之难以随后迁移到其他消息传递解决方案。如果你用很多听众来构建你的应用程序，那么选择 AMQP 或者别的东西可能会因为这个技术性的债务而变得很难或不可能。

POJO 驱动的方法意味着编写你的消息处理解决方案没有接口。

```java
@Component
public class ExampleListener {

    @JmsListener(destination = "myDestination")
    public void processOrder(String message) {
        System.out.println(message);
    }
}
```


在这个例子中，你的代码不直接绑定到任何接口。相反，将其连接到 JMS 队列的责任被移动到注释中，这更容易更新。在这个具体的例子中，你可以用 `@RabbitListener` 替换 `@JmsListener`。在其他情况下，可以使用基于 POJO 的解决方案，而不需要任何特定注释。

这只是一个例子。这并不意味着说明 JMS vs. RabbitMQ，而是代替编码的价值而不是与特定接口绑定。通过使用 **Plain Old Java Object**，你的代码可以简单得多。这有助于更好的测试，灵活性和今后做出新决策的能力。

Spring 框架及其各种投资组合项目总是旨在减少代码与现有库之间的耦合。这是依赖注入的一个主要概念，你的服务使用方式应该是连接应用程序而不是服务本身的一部分。

[原文链接。](https://spring.io/understanding/POJO#understanding-pojos)