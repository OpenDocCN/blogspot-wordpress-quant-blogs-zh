<!--yml

分类：未分类

日期：2024 年 05 月 18 日 06:24:30

-->

# FSM 和事件溯源 | 交易台的故事

> 来源：[`mdavey.wordpress.com/2013/05/28/fsm-and-event-sourcing/#0001-01-01`](https://mdavey.wordpress.com/2013/05/28/fsm-and-event-sourcing/#0001-01-01)

## FSM 和事件溯源

有一段时间，我一直在思索利用有限状态机（FSM）和事件溯源解决各种金融问题的各种概念验证（PoCs）。所以很高兴能阅读到其他人在类似领域所做的事情。虽然有些老旧，但 Ruminations of a Programmer 在使用 Akka 与事件溯源和 FSM 方面有有趣的阅读。更好的是，这篇[帖子](http://debasishg.blogspot.co.uk/2012/01/event-sourcing-akka-fsms-and-functional.html)提供了一个来自交易角度的例子🙂 Debasish 在 Emerging Technologies For The Enterprise [conference](http://phillyemergingtech.com/2012/sessions/building-applications-with-functional-domain-models-event-sourcing-and-actors)上有一个[演讲](http://phillyemergingtech.com/2012/system/presentations/debasish_ghosh-phillyete-12.pdf)，提供了更多阅读材料。

CQRS 作为事件溯源的一个原则，加上 FSM，为解决全球分布式事件问题提供了有趣的解决方案。利用[命令模型](http://martinfowler.com/bliki/CQRS.html)（FSM）与查询模型（事件[来源](http://martinfowler.com/eaaDev/EventSourcing.html)）允许[构建](http://architects.dzone.com/news/asynchronous-event-sourcing)可靠的分布式系统，在全球范围内，在某些[点](http://www.allthingsdistributed.com/2008/12/eventually_consistent.html)有意义，并且需要，但是如果通过可靠的传输实现了异步通信，那么这是可以接受的。

~ 由 mdavey 于 2013 年 5 月 28 日发布。

发表在[云](https://mdavey.wordpress.com/category/hpc/cloud/)中

标签：[事件溯源](https://mdavey.wordpress.com/tag/eventsourcing/)，[FSM](https://mdavey.wordpress.com/tag/fsm/)
