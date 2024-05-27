<!--yml

分类：未分类

日期：2024-05-18 05:33:16

-->

# 机器学习：Spark 与 Flink 对比 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2016/04/26/machine-learning-spark-vs-flink/#0001-01-01`](https://mdavey.wordpress.com/2016/04/26/machine-learning-spark-vs-flink/#0001-01-01)

## 机器学习：Spark 与 Flink 对比

来自 Capital One 的有趣幻灯片：[比较](http://www.slideshare.net/sbaltagi/flink-vs-spark) Flink 与 Spark。H2O 有 Spark 集成，通过 [SparkingWater](http://www.h2o.ai/product/sparkling-water/) 这一切都很好，但 Flink 看起来更有趣:)

没有做太多与 [TensorFlow](https://www.tensorflow.org/) 相关的工作，我看到它有自己的集群进行 [分布式](https://www.tensorflow.org/versions/r0.8/how_tos/distributed/index.html#distributed-tensorflow) 处理。然而，[databricks](https://databricks.com/blog/2016/01/25/deep-learning-with-spark-and-tensorflow.html) 已经将其与 [Spark](https://www.infoq.com/news/2016/03/databricks-spark-tensorflow/) 集成。

[Deeplearning4j](http://deeplearning4j.org/) 提供了一个有趣的[比较](http://deeplearning4j.org/compare-dl4j-torch7-pylearn.html)多个 ML 库，提到了 Spark，但没有提到 Flink。

有一些 Spark 和 Flink 的基准测试[在这里](http://sparkbigdata.com/102-spark-blog-slim-baltagi/14-results-of-a-benchmark-between-apache-flink-and-apache-spark)，在很多方面都得到了预期的结果：

> Apache Flink 在处理机器学习和图算法以及关系查询方面优于 Apache Spark，但在批处理方面却不占优势！

经过一些搜索，我们找到了 [Full Metal](http://bigstep.com/full-metal-data-lake) 数据湖。有趣的是，但这并不是我想要的东西。然而，它确实让我想到了 Apache [Drill](https://drill.apache.org/)。

“数据湖架构[考虑](http://dataottam.com/2016/02/13/data-lake-architecture-considerations-composition/)与组成”为数据湖架构提供了方向，该架构由三层和三层组成。非常有帮助，这是我在数据湖方面找到的比较好的一篇文章之一。也许也值得一读“数据湖与数据仓库的第二版对比”

回到 Flink，Zalando 的下一代数据集成和分发平台 Saiki 在 [架构](https://tech.zalando.com/blog/apache-showdown-flink-vs.-spark/) 上提供了一些思考。很高兴看到 Saiki 的统一日志使用 Apache Kafka 喂养数据湖——这是一个很好的选择:)

~ 由 mdavey 于 2016 年 4 月 26 日发表。

发布在[数据](https://mdavey.wordpress.com/category/data/)，[未分类](https://mdavey.wordpress.com/category/uncategorized/)

标签：[ApacheFlink](https://mdavey.wordpress.com/tag/apacheflink/)，[大数据](https://mdavey.wordpress.com/tag/bigdata/)，[数据湖](https://mdavey.wordpress.com/tag/datalake/)，[机器学习](https://mdavey.wordpress.com/tag/machinelearning/)
