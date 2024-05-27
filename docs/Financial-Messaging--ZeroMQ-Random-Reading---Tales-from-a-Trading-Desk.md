<!--yml

类别：未分类

日期：2024 年 5 月 18 日 06:37:01

-->

# 金融消息：ZeroMQ 随机阅读 | 交易台故事

> 来源：[`mdavey.wordpress.com/2012/08/01/financial-messaging-zeromq-random-reading/#0001-01-01`](https://mdavey.wordpress.com/2012/08/01/financial-messaging-zeromq-random-reading/#0001-01-01)

有点类似于意大利面的帖子，但可能在未来相关 😉

尽管年代久远，使用高级消息队列协议 (AMQP) 在 InfiniBand 上设计和评估金融应用基准的报告在 Martin 对 disruptor、Ultra Messaging 和 ZeroMQ (ØMQ) 的评论背景下仍值得一读

> 我们评估消息提供者时，0MQ 还不存在。这是关于
> 
> 3 年前。对于某些用例确实很有趣。
> 
> 当需要极低延迟时，您需要选择一种传输方式
> 
> 使用 IP 多播或 InfiniBand。TCP 有很大的开销，并且
> 
> 缓冲，这不适合低延迟。此外
> 
> 选择一个不使用守护程序/代理的传输方式非常重要。
> 
> 这些"中间人"增加了延迟，并且可能成为单点故障。
> 
> 失败。一跳的时间为单个微秒数是当前最先进的技术
> 
> 两个节点之间。你测量过 0MQ 吗？

这导致了福勒先生对 [LMAX](http://martinfowler.com/articles/lmax.html) 架构的概述，以及复制和主/从的细节：

> 早些时候我提到过，LMAX 在集群中运行其系统的多个副本以支持快速故障转移。复制器使这些节点保持同步。LMAX 中的所有通信都使用 IP 多播，因此客户端不需要知道哪个 IP 地址是主节点。只有主节点直接侦听输入事件并运行复制器。复制器将输入事件广播到从节点。如果主节点宕机，它的心跳丢失将被注意到，另一个节点成为主节点，开始处理输入事件，并启动其复制器。每个节点都有自己的输入 disruptor，因此有自己的日志和自己的反序列化操作。
> 
> 即使使用 IP 多播，仍然需要复制，因为 IP 消息可能以不同的顺序到达不同的节点。主节点为其余处理提供了确定的顺序。

这导致了 ZeroMQ 网站上的一些相关文章（假设您刚好想在这种情况下查看 ZeroMQ，而不想为 Ultra Messaging 付费）：

~ 由 mdavey 于 2012 年 8 月 1 日发布。

发布于 [未分类](https://mdavey.wordpress.com/category/uncategorized/)

标签：[Disruptor](https://mdavey.wordpress.com/tag/disruptor/)，[Messaging](https://mdavey.wordpress.com/tag/messaging/)
