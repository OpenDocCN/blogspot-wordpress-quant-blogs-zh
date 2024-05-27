<!--yml

类别：未分类

日期：2024-05-18 05:53:00

-->

# Akka 2.3.0 重大发布 | 来自交易台的传说

> 来源：[`mdavey.wordpress.com/2014/03/05/akka-2-3-0-major-release/#0001-01-01`](https://mdavey.wordpress.com/2014/03/05/akka-2-3-0-major-release/#0001-01-01)

## Akka 2.3.0 重大发布

很高兴看到 Akka 的下一个版本 [发布](http://typesafe.com/blog/akka-230-major-release)，其中包括以下 [关键](http://typesafe.com/blog/akka-230-major-release) 功能：

+   Akka 持久性

+   支持 Java 8

+   集群改进

+   激活模板

一些很酷的收获：

> Akka 持久性还支持事件溯源
> 
> 我们正在酝酿一些东西，它将不仅仅是管道的替代品：受 RxJava 的启发，我们正在努力实现 Akka 的反应式流，这将允许对各种流数据进行声明性转换，正确处理背压，并且当然是完全类型化的。
> 
> [actors 的分片](http://doc.akka.io/docs/akka/2.3.0/contrib/cluster-sharding.html) 在集群中。该功能的典型用例是当您有许多状态型 actors，它们一起消耗的资源（例如内存）比一个机器上能容纳的多时。您需要将它们分布在集群中的几个节点上，并且您希望能够使用它们的逻辑标识符与它们进行交互，但无需关心它们在集群中的物理位置，这也可能随时间而变化。它可能例如是在领域驱动设计术语中代表聚合根的 actors。

正如之前所博客提到的，激活模板对项目的快速启动非常棒。Akka 持久性受到欢迎。

~ 作者 mdavey，于 2014 年 3 月 5 日。

发布于 [语言](https://mdavey.wordpress.com/category/languages/) 中

标签：[akka](https://mdavey.wordpress.com/tag/akka/)
