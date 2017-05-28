---
layout: post
title: "What are AOP, Dependency Injection and Inversion Of Control"
date:   2017-05-29
excerpt: "什么是 AOP，DI，IoC"
tags: [springmvc]
comments: true
---

# Inversion of Control, IoC (控制反转)

**IoC** 是一个重要的面向对象编程的法则，用于削减代码的耦合问题。简单理解，**IoC** 可以理解为一种代码设计模式。

**IoC** 是一种设计原则，而非通用的，指的是行为规范与实际执行时的解耦。比较例如：

`myDependency.doThis()` 和 `myDependency.onEventX += doThis()` 在后者中，没有直接调用更灵活。在其一般形式中，**IoC** 涉及观察者模式，事件或回调。

# Dependency Inversion, DI (依赖反转)

**Dependency Inversion** 是另一种设计原则。粗略地说，高层抽象不应该直接取决于较低层次的抽象；这样做的结果确实在没有较低级别抽象的情况下不能重复使用高级抽象的设计。

```java
 class MyHighLevelClass {
     MyLowLevelClass dep = new MyLowLeverClass();
 }

 class App {
     void main() {  new HighLevelClass().doStuff(); }
 }
```

在这里，`MyHighLevelClass` 无法编译，无法访问 `MyLowLevelClass`。为了打破这种耦合，我们需要用一个接口来抽象低阶类，并且去除直接的实例化。

```java
class MyLowLevelClass implements MyUsefulAbstraction { ... }

class MyHighLevelClass {

    MyUsefulAbstraction dep;

    MyHighLevelClass( MyUsefulAbstraction dep ) {
        this.dep = dep;
    }
}

class App {
     void main() {  new HighLevelClass( new LowLevelClass() ).doStuff(); }
 }
```

请注意，你不需要任何特殊的容器来执行 **Dependency Inversion**，这是一个原则。

# Dependency Injection, DI (依赖注入)

简单来说，也是一种代码的设计模式，用于实现 **IoC**。**IoC** 不仅可以用依赖注入来实现，也可以用依赖查找来实现。

实现原理：在面向对象中，当 *A* 对象 (实例) 依赖 *B* 实例时，则将 *B* 的实例 (引用) 注入到 *A* 中，注入方式通常是 **constructor**、或者 **setter**。

现在依赖注入。对我来说 **Dependency Injection = IoC + Dependency Inversion**：

依赖关系在外部提供，所以我们强制执行 **Dependency Inversion** 原理。由容器设置依赖关系 (不是我们)，所以我们谈到 **IoC**。在上面提供的示例中，如果使用容器来实例化对象并在构造函数中自动注入依赖关系，那么可以执行 **Dependency Injection** (我们经常说 **DI** 容器)：

```java
class App {
     void main() {  DI.getHighLevelObject().doStuff(); }
 }
```

注意有各种形式的注入。还要注意，在这种观点下，**setter** 注入可以看作是一种回调形式 — **DI** 容器创建对象然后调用 **setter**。控制流程有效地反转。

# Aspect Oriented Programming, AOP (面向切面编程)

这是一个编程思想，其目的，也是为了代码解耦。严格来说，**AOP** 与以前的 3 点几乎没有关系。关于 **AOP** 的开创性论文非常通用，并提出将各种资源编织在一起（可能用不同语言表达）的想法，以生产工作软件。我不会在 **AOP** 上扩展更多。这里重要的是 **Dependency Injection** 和 **AOP** 的确有效地发挥了很好的作用，因为它使编织非常简单。如果使用 **IoC** 容器和 **Dependency Injection** 来抽象化对象的实例化，那么在注入依赖项之前，**IoC** 容器可以轻松地用于编织这些方面。否则将需要一个特殊的编译或一个特殊的 **ClassLoader**。


