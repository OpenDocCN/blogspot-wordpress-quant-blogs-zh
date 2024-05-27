<!--yml

分类：未分类

日期：2024-05-18 06:36:31

-->

# 更多关于 Apache Kafka 的思考——FIX 日志|交易桌面故事

> 来源：[`mdavey.wordpress.com/2012/08/08/more-thoughts-around-apache-kafka-fix-logs/#0001-01-01`](https://mdavey.wordpress.com/2012/08/08/more-thoughts-around-apache-kafka-fix-logs/#0001-01-01)

## 更多关于 Apache Kafka 的思考——FIX 日志

今年早些时候，我撰写了一篇关于 Raptor（Sungard）和实时分析的博客。这篇文章继续介绍了一些具体的 Kafka 想法：

+   Kafka 的[设计](http://incubator.apache.org/kafka/design.html)页面提供了一些用例，主要围绕“活动流”。值得注意的是提到的公司[名单](https://cwiki.apache.org/confluence/display/KAFKA/Powered+By)，这些公司正在使用 Kafka——特别是[Metamarkets](http://metamx.com/)，一家我之前在大数据分析领域撰写博客时提到过的公司。

+   对日志文件的引用特别引人注目：

> 活动流数据是任何网站报告网站使用情况的一个正常部分。活动数据比如页面浏览量、展示的内容信息、搜索等。这类东西通常通过将活动日志输出到某种文件中，然后定期汇总这些文件进行分析。

+   上述内容导致了关于 FIX 消息的思考，特别是从各种供应商那里商业可用的产品类型，例如 B2BITS 的[FIX](http://qwtradingsystem.com/documents/QWFIX/main/Getting%20Started/Features%20Tour/QWFIX%20RTAnalyzer/1.FIXMessageMonitoring.htm)日志[分析器](http://www.b2bits.com/trading_solutions/fix_log_analyzers.html)。

+   OnixS FIX Analyzer 又类似，监控日志[文件](http://www.onixs.biz/fix-analyser.html)

+   上述所有内容都导致了利用 Kafka 实时处理 FIX 日志文件。

+   Log4j 的[appender](http://incubator.apache.org/kafka/quickstart.html)如这里所示，应该从应用程序的角度使事情变得容易

+   同样，Hadoop 的[消费者](https://github.com/kafka-dev/kafka/tree/master/contrib/hadoop-consumer)提供了一些有趣的可能

此外，假设你现在有了这些数据，统计 FIX 消息可能有趣，这[可能](http://www.slideshare.net/dave_revell/nearrealtime-analytics-with-kafka-and-hbase#)引导我们到了[数据立方体](https://github.com/urbanairship/datacube)(由 HBase 支持)。

[Storm](http://www.slideshare.net/Hadoop_Summit/realtime-analytics-with-storm)也提供了与 FIX 消息有趣的[可能性](https://github.com/nathanmarz/storm/wiki/Kestrel-and-Storm)——另一篇文章。

~ mdavey 于 2012 年 8 月 8 日。

发布在[未分类](https://mdavey.wordpress.com/category/uncategorized/)

标签：[消息传递](https://mdavey.wordpress.com/tag/messaging/)
