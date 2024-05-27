<!--yml

类别：未分类

日期：2024-05-18 04:49:30

-->

# Magmasystems 博客：重返 Java 世界的漫游

> 来源：[`magmasystems.blogspot.com/2011/08/excursions-back-into-world-of-java.html#0001-01-01`](http://magmasystems.blogspot.com/2011/08/excursions-back-into-world-of-java.html#0001-01-01)

当它刚出来时，我确实做了一些 Java 开发。我发誓我做了。甚至在 1990 年代末，我在 AT&T 的一个分部 Bellcore 教授过 Java 课程。

我管理过拥有 Java 基础系统的团队。作为 CEP 系统的一部分，我不得不去编写基于 Java 的 Web 服务，并提供 Java API，以便其他团队可以连接到通知服务。

尽管如此，由于我与微软技术有着长期的历史，我通常被看作是“Dot Net  guy”。

所以，这周，我再次翻出了 Java 手册，决定用 Java 1.6 编写我小项目中的 Exchange Simulator 部分。编写模拟器相当容易，很快，我就让 FIX 消息在我的基于 Java 的 Exchange Simulator 和我的基于 .NET 的 OMS 之间传递。

Java 与 C# 并没有太大区别。他们甚至有 Reflection，这是我在过去一年里不得不做 C++ 时非常怀念的东西。我希望 Java 支持 C# 自动属性 和 C# 事件（这些功能会在 Java 1.8 中出现吗？），除此之外，感觉就像在编程 C# 1.0。

然而，Java 语言只是成为一个真正的 Java 开发者和架构师的一小部分。围绕 Java 开发有一个完整的生态系统。我从一位朋友那里列出了要学习的工具和框架，里面有很多东西。这是一个人需要的 basic 工具列表：

+   JDK 1.6

+   Eclipse 3.6（Java EE 版）

+   JTA/JTS（事务服务）

+   Spring 3.0 或 3.1

+   Hibernate 3.6

+   Open JMS 或 ActiveMQ

+   JBoss、[Jetty](http://www.eclipse.org/jetty/) 或 Apache Geronimo

+   Subversion

+   Jenkins 或 Hudson

过去的一年里，我一直在用 Eclipse 进行 C++ 开发，在 Windows 上编辑，在 Linux 上编译。使用 Eclipse 编辑、构建和调试 Java 应用程序似乎轻而易举。Eclipse 有很多我习惯于在 Visual Studio 中的 Resharper 中的实时错误检测功能。增量编译很有帮助，从编辑到运行一个应用程序几乎不需要任何时间。

多年来，我尝试了各种形式的 Spring（主要是 Spring.Net），此外还编写了自己的依赖注入框架。最近，我的 Prism 经验让我重新回到了 IOC 的世界（尽管当应用程序关闭时，模块被卸载时，我感到烦恼的是 Prism/UnityContainer 不支持任何形式的“IDisposable”模式）。由于一些记录依赖项，我无法将 Spring 3.1 整合到我的应用程序中（QuickFix/J 使用 SLF4J，这与 Spring 不兼容）。

(N)Hibernate 也是我在这些年里研究过的另一个 ORM。

至于源代码控制，我一直使用 TFS/Perforce。过去一年半的时间我都在用 Clearcase，这看起来有点古老，尽管它似乎还在工作。许多人似乎更喜欢 Subversion，所以这是一个学习它的好机会。

对于持续集成服务器也是如此。我一直使用 Cruise Control .NET 来处理我的所有 CI 需求，而 Hudson/Jenkins 是我听说了一段时间的东西。

这个栈中唯一缺失的部分是

[对我来说完全是陌生的](http://stackoverflow.com/questions/3954614/why-does-java-apps-need-an-application-server-and-net-just-iis-web-server)

是 Java 应用服务器。Java 应用服务器的整个概念对我来说有些陌生，因为我们.NET 世界中确实没有与之相当的东西。我对这些容器中的 Web 服务器功能不感兴趣，因此我需要找出我可以利用的其他功能。今天早上，我打算先下载 JBoss。

(更新 - 看起来你需要购买一个 99 美元的 JBoss 订阅。所以，我会下载 Jetty，尽管我不确定 Jetty 是否是一个完整的 Java 应用服务器。)

(源自 Stack Overflow 的一篇帖子，那里对 JAS 有一个很好的总结：

*Java EE 应用服务器是对分布式组件进行事务监控的工具。它提供了一系列抽象概念（例如，命名、池化、组件生命周期、持久化、消息传递等）以帮助实现这一目标。* *许多这些服务都是 Windows 操作系统的组成部分。Java EE 需要这些抽象概念，因为它与操作系统无关。*

我会随时向大家通报我的进展。

©2011 Marc Adler - 版权所有。在这里表达的所有观点纯属个人，与我的雇主无关。
