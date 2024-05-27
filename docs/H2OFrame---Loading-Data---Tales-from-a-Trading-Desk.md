<!--yml

类别：未分类

日期：2024 年 5 月 18 日 05:33:20

-->

# H2OFrame - 加载数据 | 交易台传奇

> 来源：[`mdavey.wordpress.com/2016/04/20/h2oframe-loading-data/#0001-01-01`](https://mdavey.wordpress.com/2016/04/20/h2oframe-loading-data/#0001-01-01)

## H2OFrame - 加载数据

“Apache [Spark](http://spark.apache.org/) 是一个用于大规模数据处理的快速通用引擎”。很明显这就是为什么 H2O 通过 [Sparkling](http://www.h2o.ai/product/sparkling-water/) Water 与 Spark 结合。这种 [集成](https://github.com/h2oai/sparkling-water) 提供：

> +   将 Spark 数据结构（RDD、DataFrame）发布为 H2O 的 frames，反之亦然的工具
> +   
> +   使用 DSL 将 Spark 数据结构作为 H2O 算法的输入。
> +   
> +   利用 Spark 和 H2O API 创建 ML 应用程序的基本构建模块
> +   
> +   Python 接口，允许直接从 pySpark 使用 Sparkling Water

“如何：使用 Sparkling Water 和 Apache Spark 构建一个机器学习应用程序” 提供了在 Spark 和 H2O 之间转换数据的见解 - 从 Spark 的弹性分布式数据集 (RDD) 到 H2OFrame，反之亦然。

H2OFrame 提供了另外一些将数据加载到 [这里](http://h2o-release.s3.amazonaws.com/h2o/master/3384/docs-website/h2o-docs/booklets/SparklingWaterVignette.pdf) 文档页面所提供的 H2OFrame 的方法：

> +   本地文件系统
> +   
> +   HDFS
> +   
> +   S3
> +   
> +   HTTP/HTTPS

因此我在想，如果数据集相对较小，那么可能更容易通过 REST 端点公开数据，而不是下载到 CVS 文件中再加载到 H2OFrame 中。也许在时间段结束时，我想要一个快照数据，我可以看到 SparklingWater 在我有数据在 hdfs 中或者我需要 Spark 集群在某个特定问题上的强大作用时的优势。然而，对于小数据集，我不确定是否需要 SparklingWater？

这导致了以下的思考过程：

+   如果你的流数据，就要决定 POJO 模型将在何处运行 - 这是 Java，所以应该很容易 - 数据订阅者。

+   如果你有大量数据，需要 SparklingWater 和集群来确保性能。

+   如果你的应用需要，RStudio 或类似的东西用于访问 H2O 就足够了

+   将流数据进行挂钩到 Apache Spark 和 H2O 似乎是不必要的，鉴于上面的第一个要点。

~ 由 mdavey 于 2016 年 4 月 20 日发布。

发布在 [Agile](https://mdavey.wordpress.com/category/agile/)

标签：[机器学习](https://mdavey.wordpress.com/tag/machinelearning/)
