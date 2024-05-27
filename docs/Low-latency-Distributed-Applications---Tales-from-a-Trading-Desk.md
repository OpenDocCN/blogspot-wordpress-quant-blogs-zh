<!--yml

分类：未分类

日期：2024-05-18 05:41:54

-->

# 低延迟分布式应用 | 交易桌面故事

> 来源：[`mdavey.wordpress.com/2015/06/09/low-latency-distributed-applications/#0001-01-01`](https://mdavey.wordpress.com/2015/06/09/low-latency-distributed-applications/#0001-01-01)

## 低延迟分布式应用

[安德鲁·布鲁克](http://queue.acm.org/detail.cfm?id=2770868)的文章“演变与实践：金融领域的低延迟分布式应用”为金融领域的低延迟问题提供了很好的阅读材料。RFQ（请求报价）和 RFS（请求服务规格）得到了适当的覆盖，同时还提到了经常被忽视的“[时钟同步](http://queue.acm.org/detail.cfm?id=2745385)”问题。此外，还讨论了线程比核心多的情况以及上下文切换的问题。

希望这类文章能帮助人们在实施低延迟架构之前了解设计过程中所做的决策，以及这些决策在生产环境中部署时可能带来的不幸结果。

还需要特别指出[Aeron 的设计原则](https://github.com/real-logic/Aeron/wiki/Design-Principles)：

> 要在最小化方差的同时实现低延迟和高吞吐量，定义一套指导开发的设计原则至关重要。当需要权衡时，这些设计原则有助于指导决策，选择相互竞争的替代方案之间的最佳方案。

没有免费的[午餐](http://www.infoq.com/presentations/java8-performance)。性能的提升需要付出代价——要么是金钱，要么是开发时间。

~ mdavey 于 2015 年 6 月 9 日。

发布在[语言](https://mdavey.wordpress.com/category/languages/)、[交易](https://mdavey.wordpress.com/category/trading/)分类下。
