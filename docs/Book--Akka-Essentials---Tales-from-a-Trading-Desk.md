<!--yml

类别：未分类

日期：2024 年 5 月 18 日 06:31:03

-->

# 书：Akka Essentials | 交易台的故事

> 来源：[`mdavey.wordpress.com/2013/01/14/book-akka-essentials/#0001-01-01`](https://mdavey.wordpress.com/2013/01/14/book-akka-essentials/#0001-01-01)

## 书：Akka Essentials

在过去的几年里，对演员模式产生了新的兴趣。 在 Microsoft 栈中，Microsoft 和 MSR 都提供了 .NET 扩展来利用演员模型。 同样，在 Java/Scala 栈中，[akka](http://akka.io/) 和 Typeseafe 已经引起了一些关注，最近发布了 akka 2.1.0。 在金融版本中，演员模型由于 sell-side 和 buy-side 中开发的系统的复杂性而受到极大关注。 因此，[Akka](http://www.amazon.co.uk/Akka-Essentials-Munish-Kumar-Gupta/dp/1849518289) [Essentials](http://www.packtpub.com/akka-java-applications-essentials/book) 出版了（对于仍然购买实体书的人）正是时候 - 尤其是如果向下滚动到 akka 主页的底部，并查看“一组生产用户”的列表 - 瑞银和瑞士信贷。

所以遵循该博客使用的历史书评格式：

+   Jonas Boner 被评论了 🙂

+   第 10 页，“编写分布式应用程序的 JEE 编程模型并不适合规模化应用程序模型”。 经典陈述。

+   第 11 页，演员原则

+   第 30 和 46 页。 Java 和 Scala 版本的同一个示例应用程序。 尽管在我看来，Scala 是开发的首选，但我们中的一些人在日常工作中不得不生活在 Java 世界中。 Java 是 21 世纪的 Cobol 吗？

+   第 74 页。 在运行时交换和演员消息循环功能的能力

+   第 90 页。 管理员策略

+   第 97 页。 通过 java.util.concurrent 进行调度程序

+   第 123 页。 让它崩溃的范式！ 在决定监督和监控时考虑机器故障是很重要的。

+   第 171 页。 久远的金钱账户转移问题，但使用 STM

+   第 248 页。 Typesafe 控制台。 如果您还没有启动控制台，请阅读本章，然后重新考虑。

因此，总结一下，如果你打算在即将到来的项目中利用 akka，那么 Akka Essentials 值得一读。 应该注意的是，Akka 2.1.0（[Coltrane](http://doc.akka.io/docs/akka/2.1.0/cluster/cluster-usage-java.html)）提供了实验性的集群支持，这对于构建生产就绪的 Akka 解决方案至关重要，因此没有在 Akka Essentials 中涵盖。

~ mdavey 于 2013 年 1 月 14 日发布。

发布在 [Java](https://mdavey.wordpress.com/category/languages/java/) 中
