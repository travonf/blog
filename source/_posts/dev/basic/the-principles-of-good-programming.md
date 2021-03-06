---
title: The Principles of Good Programming
date: 2007-09-03 08:00:00
updated: 2007-09-03 08:00:00
tags: "dev"
categories: "Develop"
---

## 编程原则

来源：https://www.artima.com/weblogs/viewpost.jsp?thread=331531

<!-- more -->

### DRY - don't repeat yourself - 不要自我重复

一旦程序里开始有重复现象的出现(例如很长的表达式、一大堆的语句，但都是为了表达相同的概念)，你就需要对代码进行一次新的提炼，抽象

### Abstraction Principle - 提炼原则

程序中任何一段具有功能性的代码在源代码文件中应该唯一的存在

### KISS - Keep it simple, stupid!

保持简单

简单化(避免复杂)永远都应该是你的头等目标。简单的程序让你写起来容易，产生的 bug 更少，更容易维护修改。

### YAGNI - ya ain't gonna need it

你不会用到它的

除非你真正需要用到它，否则不要轻易加上那些乱七八糟用不到的功能。表示程序员不应为目前还不需要的功能编写代码

### Do the simplest thing that could possibly work

用最简单的方法让程序跑起来

在开发时有个非常好的问题你需要问问自己，“怎样才能最简单的让程序跑起来？”这能帮助我们在设计时让程序保持简单。

### Don't make me think

不要让我动脑子

这实际上是 Steve Krug 关于 web 界面操作的一本书的书名，但也适用于编程。

主旨是，程序代码应该让人们花最小的努力就能读懂和理解。如果一段程序对于阅读者来说需要花费太多的努力才能理解，那它很可能需要进一步简化。

### Open/Closed Principle

开放/封闭原则

程序里的实体项(类，模块，函数等)应该对扩展行为开放，对修改行为关闭。换句话说，不要写允许别人修改的类，应该写能让人们扩展的类

### Write Code for the Maintainer

为维护者写程序

任何值得你编写的程序在将来都是值得你去维护的，也许由你维护，也许由他人。

在将来，当你不得不维护这些程序时，你对这些代码的记忆会基本上跟一个陌生人一样，所以，你最好还是当成一直在给别人写程序。

一个有助于你记住这个原则的办法是“写程序时时刻记着，这个将来要维护你写的程序的人是一个有严重暴力倾向，并且知道你住在哪里的精神变态者”。

### POLS - Principle of least surprise

最小意外原则

最少意外原则通常是使用在用户界面设计上，但这个原则同样适用于编写程序。

程序代码应尽可能的不要让阅读者感到意外。

也就是说应该遵循编码规范和常见习惯，按照公认的习惯方式进行组织和命名，不符常规的编程动作应该尽可能的避免。

### Single Responsibility Principle

单一职责原则

一个代码组件(例如类或函数)应该只执行单一的预设的任务。

### loose coupling high cohesion

高内聚低耦合

### Minimize Coupling

最小化耦合性

一个代码片段(代码块，函数，类等)应该最小化它对其它代码的依赖。这个目标通过尽可能少的使用共享变量来实现。

“低耦合是一个计算机系统结构合理、设计优秀的标志，把它与高聚合特征联合起来，会对可读性和可维护性等重要目标的实现具有重要的意义。”

### Maximize Cohesion

最大化内聚性

具有相似功能的代码应该放在同一个代码组件里。

### Hide Implementation Details

隐藏实现细节

隐藏实现细节能最小化你在修改程序组件时产生的对那些使用这个组件的其它程序模块的影响

### Law of Demeter

笛米特法则

程序组件应该只跟它的直系亲属有关系(例如继承类，内包含的对象，通过参数入口传入的对象等。)

### Avoid Premature Optimization

避免过早优化

只有当你的程序没有其它问题，只是比你预期的要慢时，你才能去考虑优化工作。

只有当其它工作都做完后，你才能考虑优化问题，而且你只应该依据经验做法来优化。

“对于小幅度的性能改进都不该考虑，要优化就应该是 97%的性能提升：过早优化是一切罪恶的根源”—Donald Knuth。

### Code Reuse is Good

代码复用

这不是非常核心的原则，但它跟其它原则一样非常有价值。代码复用能提高程序的可靠性，节省你的开发时间

### Separation of Concerns

职责分离

不同领域的功能应该由完全不同的代码模块来管理，尽量减少这样的模块之间的重叠。

### Embrace Change

拥抱变化

是 Kent Beck 的一本书的副标题，它也是极限编程和敏捷开发方法的基本信条之一。

很多的其它原则都基于此观念：面对变化，欢迎变化。事实上，一些经典的软件工程原则，例如最小化耦合，就是为了让程序更容易面对变化。

不论你是否采用了极限编程方法，这个原则对你的程序开发都有重要意义。
