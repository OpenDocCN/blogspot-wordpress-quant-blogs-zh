<!--yml

分类：未分类

日期：2024-05-18 05:37:27

-->

# Midori：细粒度进程扩展 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2015/12/02/midori-fine-grained-process-scaling/#0001-01-01`](https://mdavey.wordpress.com/2015/12/02/midori-fine-grained-process-scaling/#0001-01-01)

## Midori：细粒度进程扩展

最后，Joe [Duffy](http://joeduffyblog.com/) 重新开始博客了，随之而来的是关于[Midori](http://joeduffyblog.com/2015/11/03/blogging-about-midori/)的详细内容（编程语言，编译器，操作系统，其服务，应用程序以及整体的编程模型），这是多年的旅程。

> 实现异步处理的关键是超轻量级进程。

我很想知道 Midori 是否影响了[Orleans](http://research.microsoft.com/en-us/projects/orleans/)——考虑到两者在演员模型上的相似性。Orleans 的代码可以在[GitHub](http://dotnet.github.io/orleans/)上找到。

在“异步处理一切”这篇文章中，有很多很好的亮点：

+   Midori 没有采用按需分页，在传统的系统中，这意味着访问内存可能会物理性地阻塞以执行 I/O 操作。

+   Midori 是一个完整的操作系统，它旨在使用垃圾收集的内存——不幸的是，我们没有看到 Joe 提供 Midori 是否是一个可行的生产操作系统的观点。

+   避免不必要的分配，比如瘟疫。Gen0 收集不是免费的。

+   垃圾回收在 Midori 这样的系统中能够大规模工作，其中一个诀窍就是精细的进程模型，每个进程都有自己的堆，可以独立进行垃圾回收。

+   进程超轻量级且单线程——基于事件循环。

+   可以在通道中一次性填充大量消息，在通道满之前它们就被发送了。它们是以块为单位一次又一次地交付的——很有趣，因为类似的观念在金融软件中已经被使用了多年。

+   “零拷贝”，SharedData 是对某些不可变数据在进程间共享的堆上的自动引用计数指针。很想了解这个技术是如何跨机器工作的。

+   随消息跨进程流动的因果关系 ID。

+   无处不在的异步处理。

作者：mdavey，日期：2015 年 12 月 2 日。

发表于[.NET](https://mdavey.wordpress.com/category/languages/net/)分类下
