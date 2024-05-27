<!--yml

类别：未分类

日期：2024-05-18 04:55:48

-->

# Magmasystems Blog：IBM MQ 系列、XMS 和.NET

> 来源：[`magmasystems.blogspot.com/2009/02/ibm-mq-series-xms-and-net.html#0001-01-01`](http://magmasystems.blogspot.com/2009/02/ibm-mq-series-xms-and-net.html#0001-01-01)

我们需要读取另一个系统通过 IBM MQ 输出的信息。IBM 有一种名为 XMS 的消息实现，它看起来像是 JMS 通过 MQ 的实现。这对我们来说很好，因为这意味着我们可能（希望）能够克隆我们现有的 Tibco EMS 适配器，并进行一些小小的更改，从而能够从 MQ 读取。

我不知道原始数据发布者是否也必须使用 XMS...

也许这里有人可以告诉我

. 我确信发布系统不使用 XMS。如果发布者必须使用 XMS 以便我们通过 XMS 消费，那么我们将需要开发一个使用原生 MQ API 的输入适配器。

关于 IBM .NET 消息客户端的信息是

[这里](http://www-01.ibm.com/support/docview.wss?rs=171&uid=swg24011756)

.

更新：IBM WebSphere 预销售 Richard Brown 的精彩评论告诉我，如果我们只是消费者，那就没有什么可担心的... 我们就是。

版权所有©2009 Marc Adler。

这里的所有观点都是个人的，与我的雇主无关。
