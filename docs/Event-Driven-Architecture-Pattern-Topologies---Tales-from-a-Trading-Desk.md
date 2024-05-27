<!--yml

类别：未分类

日期：2024 年 5 月 18 日 05:43:36

-->

# 事件驱动架构模式拓扑结构 | 交易台的故事

> 来源：[`mdavey.wordpress.com/2015/03/02/event-driven-architecture-pattern-topologies/#0001-01-01`](https://mdavey.wordpress.com/2015/03/02/event-driven-architecture-pattern-topologies/#0001-01-01)

## 事件驱动架构模式拓扑结构

O’Reilly Radar 在事件驱动[架构](http://radar.oreilly.com/2015/02/variations-in-event-driven-architecture.html)方面有一篇有趣的文章，“事件驱动架构的变化”。如果您想要完整阅读，马克·理查德的电子书在[这里](https://mdavey.wordpress.com/2015/02/19/user-story-map/ "用户故事地图")可供下载。

或许值得指出的是，我遇到过很多人担心在使用中介器拓扑结构时的事件队列数量 - 在我看来是一种奇怪的思维过程，除非架构师打算使用单个队列处理所有事件类型 😦

> 在事件驱动架构中，通常会有从十几到几百个事件队列

还令人担忧的是，很多人忽略了开源的集成中心，而是直接编写自己的变体 - 缺乏投资回报率

> 事件中介器的最简单和最常见的实现是通过开源集成中心，如 Spring Integration、Apache Camel 或 Mule ESB。

在马克的电子书中看到对基于空间的架构的引用真是不错。惊讶的是，当我提到空间架构时，有多少人面无表情 😦

~ 由 mdavey 于 2015 年 3 月 2 日撰写。

发布在[交易](https://mdavey.wordpress.com/category/trading/)类别下
