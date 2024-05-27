<!--yml

category: 未分类

date: 2024-05-18 05:55:31

-->

# Vert.x Thoughts – Cluster | Tales from a Trading Desk

> 来源：[`mdavey.wordpress.com/2014/01/03/vert-x-thoughts-cluster/#0001-01-01`](https://mdavey.wordpress.com/2014/01/03/vert-x-thoughts-cluster/#0001-01-01)

## Vert.x Thoughts – Cluster

Lance 的“从集群到浏览器的异步数据”[演示](http://lanceball.com/dataIO2013/#/) 在我的看法中，第 [2](http://lanceball.com/dataIO2013/#/1) 张幻灯片上提供了信息的金矿，“应用程序平台”。如果你还没有尝试过 Vertx，我建议你下载并 [安装](http://vertx.io/install.html)。正如此前在这个博客上讨论的那样，[响应式](http://vertx.io/manual.html#asynchronous-programming-model) 是“有趣的”。如果你已经玩过 Akka，以及 Actor 模式，当你阅读 Vertx 手册上关于事件总线和 [HA](http://vertx.io/manual.html#high-availability-with-vertx)/cluster 特性时，你可能对 [Vertx](http://www.slideshare.net/wuman/development-with-vertx-an-eventdriven-application-framework-for-the-jvm) 感兴趣。分布式事件总线，覆盖一组响应式 Module/*verticles*。

> 简单的 *actor-like* 并发模型。[Vert.x](http://www.cubrid.org/blog/dev-platform/understanding-vertx-architecture-part-2/) 允许你将所有代码编写为单线程，摆脱多线程编程的许多陷阱（不再需要 `synchronized`、`volatile` 或显式锁定）。

有一些 [Vert.x](http://parleys.com/play/5148922b0364bc17fc56c8c7/chapter0/about) 示例可在 [这里](https://github.com/vert-x/vertx-examples) 获得。工作队列模块可在 [这里](https://github.com/vert-x/mod-work-queue) 获得。Mongo 持久化器可在 [这里](https://github.com/vert-x/mod-mongo-persistor) 获得。

~ 由 mdavey 在 2014 年 1 月 3 日。

发布于 [Languages](https://mdavey.wordpress.com/category/languages/)

标签：[Vertx](https://mdavey.wordpress.com/tag/vertx/)
