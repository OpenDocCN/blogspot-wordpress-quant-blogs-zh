<!--yml

分类：未分类

日期：2024-05-18 05:33:46

-->

# 将数据流式传输到 H2o | 交易桌旁的故事

> 来源：[`mdavey.wordpress.com/2016/04/20/streaming-data-into-h2o/#0001-01-01`](https://mdavey.wordpress.com/2016/04/20/streaming-data-into-h2o/#0001-01-01)

## 将数据流式传输到 H2o

这不是一个广泛公开宣传的内容，鉴于我们如今生活在实时世界中，这在我看来很奇怪，但在网上搜索后，我在 H2O World 2015 培训 [网站](http://learn.h2o.ai/content/tutorials/streaming/storm/index.html) 上找到了一篇相关文章。

+   databrick [流式处理](https://databricks.com/blog/category/engineering/streaming)

+   深入探讨 Spark Streaming 的[执行模型](https://databricks.com/blog/2015/07/30/diving-into-spark-streamings-execution-model.html)

+   对 Kafka [集成](https://databricks.com/blog/2015/03/30/improvements-to-kafka-integration-of-spark-streaming.html) 的改进

+   如何构建：使用 Sparkling Water 和 Apache [Spark](http://blog.cloudera.com/blog/2015/10/how-to-build-a-machine-learning-app-using-sparkling-water-and-apache-spark/) 构建机器学习应用

使用 H2O 在 [Storm](http://learn.h2o.ai/content/tutorials/streaming/storm/index.html) 上进行实时预测并不是我想要找的，我更感兴趣的是 Apache Kafka。然而，它足够接近我要解决的问题，是有用的 🙂

源代码可以在 [这里](https://github.com/h2oai/h2o-tutorials/tree/master/tutorials/streaming/storm) 找到。TestH2ODataSpout.java 是假实时数据。 [H2OStormStarter.java](https://github.com/h2oai/h2o-tutorials/blob/master/tutorials/streaming/storm/H2OStormStarter.java) 是有趣的代码，它消耗实时数据，并通过收集器的 emit() 和 ack() 函数输出结果。

预测 bolt 通过收集器发出元组到 ClassifierBolt，后者将数据写入文件（out）并也将分类结果发到收集器。

窍门是 ClassifierBolt 写入一个文件（out），这被 JS 代码读取。实际上 ClassifierBolt 的结果可能应该通过 websocket 传输到 HTML 用户界面。

净输出，使用 Storm、Kafka 或其他技术无关紧要，关键是将模型作为 Java POJO 通过 R 导出，然后使用 h2o.download_pojo()。

~ 由 mdavey 于 2016 年 4 月 20 日发表。

发布在 [数据](https://mdavey.wordpress.com/category/data/)

标签：[H2O](https://mdavey.wordpress.com/tag/h2o/)，[Kafka](https://mdavey.wordpress.com/tag/kafka/)，[机器学习](https://mdavey.wordpress.com/tag/machinelearning/)
