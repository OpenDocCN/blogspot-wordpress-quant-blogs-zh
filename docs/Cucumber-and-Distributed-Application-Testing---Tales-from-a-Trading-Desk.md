<!--yml

类别：未分类

日期：2024 年 5 月 18 日 06:25:47

-->

# 黄瓜和分布式应用测试 | 来自交易台的传说

> 来源：[`mdavey.wordpress.com/2013/05/06/cucumber-and-distributed-application-testing/#0001-01-01`](https://mdavey.wordpress.com/2013/05/06/cucumber-and-distributed-application-testing/#0001-01-01)

## 黄瓜和分布式应用测试

编写分布式应用程序很复杂。测试分布式应用程序同样复杂。将跨越 LAN/WAN 的分布式应用程序与延迟影响联系在一起，软件工程/测试的复杂性变得相当令人头疼。

在我看来，黄瓜之所以好，是因为它允许以纯文本和业务 DSL 编写测试。不久前，当我编写分布式应用程序并尝试编写黄瓜测试时，我意识到我可以从我绘制的序列[图](http://www.cs.sjsu.edu/~pearce/modules/lectures/ooa/analysis/ecb.htm)（[PlantUML](http://plantuml.sourceforge.net/sequence.html)）中受益，以便我可以可视化我概念验证（PoC）中各方（节点）之间的消息流。

我的想法是让黄瓜将序列图包含在“Then”子句中，以帮助验证应该在节点之间流动的消息。这个简单而几乎显而易见的想法，导致了以下黄瓜场景（利用 Eugene 的[示例](http://eprystupa.wordpress.com/2012/12/23/prototyping-a-matching-engine-with-scala-and-cucumber/)）：

```
Scenario: Add two limit orders to the SELL order book, with more aggressive order first
    When the following orders are added to the "Sell" book:
      | Broker | Qty | Price |
      | A      | 100 | 10.6  |
      | B      | 100 | 10.7  |
    Then the "Sell" order book looks like:
      | Broker | Qty | Price |
      | A      | 100 | 10.6  |
      | B      | 100 | 10.7  |
    And the Message flow looks like:
      @startuml
       actor BrokerA
       actor BrokerB
       boundary MatchingEngine
       BrokerA --> MatchingEngine: LimitOrder
       BrokerB --> MatchingEngine: LimitOrder
      @enduml

```

如你所见，黄瓜场景有效地让我验证了完成状态，还有传递给创建状态的消息。对于特定类型的构建在有限状态机（[FSM](https://en.wikipedia.org/wiki/Finite-state_machine)）之上的分布式应用程序，在全球分布的应用程序中，该场景不仅允许基于状态进行一定程度的信心，还允许基于在 WAN/LAN 上传递的消息来构建每个节点的状态。

现有一些 [PlantUML](http://plantuml.sourceforge.net/sequence.html) 解析器可供使用，其中之一是 [Intellij-puml](https://github.com/Stefku/intellij-puml)，如果你恰好想要深入了解，这个工具可以帮助你。

作者：mdavey，2013 年 5 月 6 日发布。

发布于 [云](https://mdavey.wordpress.com/category/hpc/cloud/)，[Java](https://mdavey.wordpress.com/category/languages/java/)

标签：[黄瓜](https://mdavey.wordpress.com/tag/cucumber/)
