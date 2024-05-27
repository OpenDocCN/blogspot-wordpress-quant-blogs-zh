<!--yml

分类：未分类

日期：2024-05-18 06:36:53

-->

# 市场数据 – 大数据思考 | 交易桌面故事

> 来源：[`mdavey.wordpress.com/2012/08/02/market-data-big-data-thoughts/#0001-01-01`](https://mdavey.wordpress.com/2012/08/02/market-data-big-data-thoughts/#0001-01-01)

exegy 的市场数据高峰（ both [欧洲](http://www.marketdatapeaks.eu) 和 [美国](http://www.marketdatapeaks.com/)）提供了一个很好的提醒，总体金融服务业的大数据问题中市场数据的数量。除了市场数据，还有不断增长的订单/交易数据和风险数据。正如之前博客中提到的，数据增长只会上升。

因此，总是有趣地看到在大数据领域推出新产品。上个月[Nodeable](http://www.nodeable.com/) [推出了](http://techcrunch.com/2012/07/18/twitter-storm-nodeable-pivot/) StreamReduce。StreamReduce 很有趣，因为它的核心是 Storm。Storm 存在于与“复杂事件处理”（CEP）系统相同的领域，如[Esper](http://esper.codehaus.org/)，[Streambase](http://www.streambase.com/)，微软 StreamInsight（我几年前 extensively blogged about）和[S4](http://s4.io/)。StreamReduce 基本上是[Storm](http://engineering.twitter.com/2011/08/storm-is-coming-more-details-and-plans.html)在云中，还有一些额外的功能，如连接到 Apache Hadoop 的连接器。

> **侧边栏**：太好看了 Nodeable 上的那些熟悉的 JavaScript 库 “2012 年的 JavaScript 柱石” [帖子](http://blog.nodeable.com/2012/07/27/the-javascript-pillars-of-2012/)

在大数据的早期，hadoop 是王者，批处理是前进的道路。然而，像许多软件工程道路一样，我们已经超过了批处理[处理](http://blog.nodeable.com/2012/07/02/when-hadoop-isnt-fast-enough-the-argument-for-storm/)，现在在一个实时（或近乎实时）的世界里，这基本上使我们到达 CEP 作为大数据分析的支柱。Storm 和 S4 在网络上获得了大量关注，有些人 debate as to which is the [更好](http://www.quora.com/What-would-you-choose-between-Flume-Yahoo-S4-and-Backtype-Twitter-Storm-and-why) of the [two](https://groups.google.com/forum/?fromgroups#!topic/s4-project/aRr-_RiB4Zc)。Yahoo Labs 有一个相当古老，但实用的[阅读](http://labs.yahoo.com/node/476)关于 S4 - 分布式流计算平台：

> S4 是一个通用、分布式、可扩展、部分容错、可插拔的平台，允许程序员轻松地开发处理连续的不受限数据流的程序。带键的数据事件与处理元素（PEs）具有亲缘关系进行路由，这些处理元素消耗事件并执行以下一项或两项：（1）发出一个或多个可能被其他 PEs 消耗的事件；（2）发布结果。该架构类似于演员模型[1]，提供了封装和位置透明的语义，从而允许应用程序在大量并发的情况下运行，同时向应用程序开发者暴露一个简单的编程接口。在这篇论文中，我们详细概述了 S4 架构，描述了各种应用，包括实际部署。我们的设计主要受制于生产环境中的大数据挖掘和机器学习的大型应用。我们展示了 S4 设计非常灵活，并且可以运行在由商用硬件构建的大型集群中。

所以如果 CEP 是大数据的支柱之一，那么其他的可能包括存储和可视化/分析。在大数据存储领域，Cassandra 是众多竞争者之一。Acunu 提供了一个 Cassandra[变种](http://www.acunu.com/2/post/2012/07/really-big-data.html)，根据 Acunu 的网站暗示，客户可能使用了 Storm：

> Storm，MQ 和其他事件框架与 Acunu Reflex 很好地结合在一起[分析](http://www.acunu.com/acunu-analytics.html)。你可以使用它们来预处理或过滤传入的数据，然后使用 Acunu 进行处理、存储并向前端应用程序提供服务。

2010/11 年的 Metamarkets 清楚地认为当时的关系数据库和 NoSQL 技术产品不适合大数据，当他们用自己的方式[Druid](http://metamarkets.com/2011/druid-part-i-real-time-analytics-at-a-billion-rows-per-second/)，利用与 Twitter 的[Rainbird](http://www.slideshare.net/kevinweil/rainbird-realtime-analytics-at-twitter-strata-2011)非常相似的数据存储模式时。Metamarkets 的设计架构原则[很有趣](http://metamarkets.com/2011/druid-part-deux-three-principles-for-fast-distributed-olap/)。第二个和第三个原则是可以预料的，使用 Zookeeper 进行协调。第一个原则特别是关于部分聚合是最有趣的。

最后，以可视化来结束。如果我们从 R 语言开始，Metamarkets 再次为我们提供了一些[见解](http://metamarkets.com/2012/munging-and-visualizing-data-with-r/)。DataStax[和](http://www.analyticbridge.com/profiles/blogs/datastax-and-pentaho-jointly-deliver-complete-analytics-solution-)Pentaho 提供了一个基于网页界面的 Cassandra 解决方案，可以互动地分析、可视化大数据，然后生成报告和创建[仪表板](http://www.pentahobigdata.com/ecosystem/capabilities/analytics)。然而，尚不清楚这个网页解决方案的实时性如何，以及是否利用 WebSockets 来促进互联网数据的流式传输。我怀疑 Pentaho 的可视化解决方案将不支持交易台对于实时数据交易/风险钻取的通常要求。

~ mdavey 于 2012 年 8 月 2 日。

发布于：[复杂事件处理](https://mdavey.wordpress.com/category/hpc/cep/)，[云计算](https://mdavey.wordpress.com/category/hpc/cloud/)

标签： [大数据](https://mdavey.wordpress.com/tag/bigdata/)
