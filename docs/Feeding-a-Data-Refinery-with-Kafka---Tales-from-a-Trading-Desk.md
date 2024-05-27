<!--yml

类别：未分类

日期：2024-05-18 05:35:45

-->

# 使用 Kafka 为数据精炼厂提供数据 | 来自交易台的故事

> 来源：[`mdavey.wordpress.com/2016/03/11/feeding-a-data-refinery-with-kafka/#0001-01-01`](https://mdavey.wordpress.com/2016/03/11/feeding-a-data-refinery-with-kafka/#0001-01-01)

## 使用 Kafka 为数据精炼厂提供数据

接着之前关于[数据精炼厂](https://mdavey.wordpress.com/2016/01/21/real-time-data-refinery/)的帖子，我现在开始考虑将[Kafka](http://kafka.apache.org/) （我的分布式提交日志）连接到 H2O。基于短时间使用 R-Studio 觉得[H2O](http://www.h2o.ai/)有趣，再加上[分析](http://hortonworks.com/hadoop-tutorial/predictive-analytics-h2o-hortonworks-data-platform/)的可用性，以及平台的普遍接受程度 - 我错了吗？

我在 Google 上找不到很多关于连接 Kafka 到 H2O 的内容。因此，我在想是否应该考虑将 Kafka 连接到 Spark，从而使用[Sparking Water](http://www.h2o.ai/product/sparkling-water/)？Spark 提供了一些[连接](http://spark.apache.org/docs/latest/streaming-kafka-integration.html)到 Kafka 的选项：

1.  基于接收者的方法

1.  直接方法（无接收者）

无接收者方法似乎是首选，其好处是数据丢失为零 - 总是一件好事 🙂

更进一步，我想知道如果我将技能云与其他有趣的“数据”连接起来，我可以预测出什么。按照云技能[帖子](https://mdavey.wordpress.com/2014/06/03/skill-cloud-part-3/)的说法。

~ 由 mdavey 于 2016 年 3 月 11 日发布。

发表在[云](https://mdavey.wordpress.com/category/hpc/cloud/)，[数据](https://mdavey.wordpress.com/category/data/)，[Java](https://mdavey.wordpress.com/category/languages/java/)，[语言](https://mdavey.wordpress.com/category/languages/)领域
