<!--yml

分类：未分类

日期：2024-05-18 05:56:36

-->

# 流式大数据查询处理管道：Storm、Cassandra、Kafka | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2013/12/11/in-stream-big-data-query-processing-pipeline-storm-cassandra-kafka/#0001-01-01`](https://mdavey.wordpress.com/2013/12/11/in-stream-big-data-query-processing-pipeline-storm-cassandra-kafka/#0001-01-01)

## 流式大数据查询处理管道：Storm、Cassandra、Kafka

关于批量导向数据处理缺点的有趣[阅读](http://highlyscalable.wordpress.com/2013/08/20/in-stream-big-data-processing/)在 Highly Scalable 上讨论了。数据分区和小范围移动被视为大数据集的解决方案。血统追踪也进行了讨论🙂文章以简要概述使用 Storm、Cassandra 和 Kafka 构建的解决方案结束：

> 系统自然地使用 Kafka 0.8 作为分区的容错事件缓冲区，以实现流重放和通过轻松添加新的事件生产者和消费者来提高系统可扩展性。Kafka 回滚读指针的能力也使得可以随机访问传入的批次，进而实现 Spark 风格的血统追踪。还可以将系统输入指向 HDFS 以处理历史数据。
> 
> 如早先所述，Cassandra 用于状态检查点和本地聚合。在许多用例中，它还存储最终结果。
> 
> 推特的 Storm 是系统的骨架。所有活跃的查询处理都在与 Kafka 和 Cassandra 交互的 Storm 拓扑中进行。一些数据流程简单直接：数据到达 Kafka；Storm 读取并处理它，并将结果持久化到 Cassandra 或其他目的地。其他的流程则更为复杂：一个 Storm 拓扑可以通过 Kafka 或 Cassandra 将数据传递给另一个拓扑。

在迈向统一的大数据处理过程中，正如文章所指出的，Apache Spark 引起了人们的兴趣——流式样本[在此](https://github.com/apache/incubator-spark/tree/master/examples/src/main/java/org/apache/spark/streaming/examples)。

~ mdavey 于 2013 年 12 月 11 日。

发布在[数据](https://mdavey.wordpress.com/category/data/)分类下。
