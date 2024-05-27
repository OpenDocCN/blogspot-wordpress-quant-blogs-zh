<!--yml

分类：未分类

日期：2024-05-18 06:34:54

-->

# Scala IDE – Versions are Too Painful | Tales from a Trading Desk

> 来源：[`mdavey.wordpress.com/2012/09/27/scala-ide-versions-are-too-painful/#0001-01-01`](https://mdavey.wordpress.com/2012/09/27/scala-ide-versions-are-too-painful/#0001-01-01)

## Scala IDE – Versions are Too Painful

在过去的几个晚上，我一直在用 Scala 做一些工作。起初，我选择 [Eclipse](http://scala-ide.org/docs/user/gettingstarted.html) 作为开发环境。但后来我想起我有多不喜欢 Eclipse，于是转投到了 [IntelliJ](http://www.jetbrains.com/idea/)。我更喜欢 IntelliJ 的重构支持，但对于某些原因，我发现用 Scala 进行运行/调试特别痛苦，所以最终又回到了 Eclipse。安装了 [ScalaIDE](http://scala-ide.org/docs/user/gettingstarted.html) 后（因此也安装了 Scala 2.9.2），我体验到了创建 [Maven](http://www.stupiphany.org/?p=10) Scala 项目的挫折，并发现 MySpec 测试无法构建。后来发现，无论是正确还是错误，解决方案都是要修正 scala-library、junit 和 specs 的 pom.xml 文件。其中 [Specs](http://code.google.com/p/specs/) 可能是关键，因此转而使用 [Specs2](http://etorreborre.github.com/specs2/)。这让我想起了之前写过的观点，即在 2012 年，IDE 和版本搭配仍然痛苦不堪。开发环境的搭建和开发工作的开始不应该这么困难。😦

如果有人稍微好奇的话，我目前使用的是 Scala 2.9.2，JUnit 4.8.1 和 Specs2 1.12.1

~ by mdavey on September 27, 2012.

发布于 [Java](https://mdavey.wordpress.com/category/languages/java/) 分类下
