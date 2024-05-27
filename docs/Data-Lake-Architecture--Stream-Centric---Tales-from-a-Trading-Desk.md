<!--yml

类别：未分类

日期：2024 年 05 月 18 日 05:33:37

--> 

# 数据湖架构：流为中心 | 来自交易台的故事

> 来源：[`mdavey.wordpress.com/2016/04/26/data-lake-architecture-stream-centric/#0001-01-01`](https://mdavey.wordpress.com/2016/04/26/data-lake-architecture-stream-centric/#0001-01-01)

## 数据湖架构：流为中心

有许多种方法可以创建和填充您的数据湖。一个特别有趣的主题是利用 Apache Kafka，该主题在“利用 Apache Kafka：构建流数据[平台](http://www.confluent.io/blog/stream-data-platform-1/)”中得到了很好的记录。文章很好地解释了特定的方法：

> “根据需要在系统和应用程序之间进行管道传输，并将任何异步处理塞入请求-响应 Web 服务。”

这变成了一个有趣的[图表](http://cdn2.hubspot.net/hub/540072/file-3062870508-png/blog-files/data-flow-ugly.png) 🙂

文章随后进入了第 2 版，名为“Kafka 东西”，它具有改进的[架构](http://cdn2.hubspot.net/hub/540072/file-3062870518-png/blog-files/stream_data_platform.png)，具有明确定义的流和模式 - “流为中心的数据架构”，以及以下好处：

1.  > **数据集成**：流数据平台捕获事件流或数据更改流，并将其馈送到其他数据系统，如关系型数据库、键值存储、Hadoop 或数据仓库。
1.  > 
1.  > **流处理**：它实现了对这些流的持续、实时处理和转换，并将结果在整个系统范围内可用。

在利用[H2O](http://www.h2o.ai/)的情况下，这提供了通过在 Apache Spark 和数据湖（HDFS）上使用 SparkingWater 以及通过 H2O POJO 的 Apache Kafka 流进行实时推送业务洞察力到用户体验的机会。

[两篇](http://www.confluent.io/blog/stream-data-platform-1/) [文章](http://www.confluent.io/blog/stream-data-platform-2/) 都值得一读。

如果有读者发现了比 Apache Kafka 更好的解决数据[湖](http://searchbusinessanalytics.techtarget.com/feature/Building-a-data-lake-architecture-can-drag-unprepared-users-under)数据集成问题的方法，以及相同的机器学习解决方案，我们会很感兴趣。

~ 作者：mdavey，2016 年 4 月 26 日。

发布在[数据](https://mdavey.wordpress.com/category/data/)类别中。

标签：[数据湖](https://mdavey.wordpress.com/tag/datalake/)，[机器学习](https://mdavey.wordpress.com/tag/machinelearning/)
