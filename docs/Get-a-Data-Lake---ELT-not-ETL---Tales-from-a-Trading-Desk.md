<!--yml

分类: 未分类

日期: 2024-05-18 05:33:24

-->

# 获取一个数据湖 - ELT 不是 ETL | 来自交易台的故事

> 来源：[`mdavey.wordpress.com/2016/04/24/get-a-data-lake-elt-not-etl/#0001-01-01`](https://mdavey.wordpress.com/2016/04/24/get-a-data-lake-elt-not-etl/#0001-01-01)

## 获取一个数据湖 - ELT 不是 ETL

[数据湖](http://www.blue-granite.com/blog/bid/402596/Top-Five-Differences-between-Data-Lakes-and-Data-Warehouses)是“大数据”时代流传甚广的一个词。许多[公司](https://spark-summit.org/2015/events/a-big-data-lake-based-on-spark-for-bbva-bank/)/人已经弄清楚了数据湖是什么，已经创建了数据湖，并且正在有效地利用它。其他人仍然[困惑](http://www.snowflake.net/blog/data-lake-or-data-swamp/)或不确定。

当今有许多文章和博客帖子让人对数据湖有了更清晰的认识。这里有[一个](http://www.infoq.com/articles/cazena-big-data-as-a-service)定义：

> 数据湖是用于存储和处理大量数据的数据存储库。通常用于在将数据集用于分析之前以原始格式收集原始数据。

从很多方面来看，这导致了一个关键的观点，“ELT 不是 ETL” - 感谢 James Serra 的[发布](http://www.jamesserra.com/archive/2015/04/what-is-a-data-lake/)。

> ELT 而不是 ETL（将数据加载到数据湖然后处理它）。这可以加快转换的速度，因为数据湖通常位于可以比 ETL 工具更快地转换数据的 Hadoop 集群中

这引导我们确定组织中所有数据源，决定如何从这些源中最佳地提取和加载数据-电子表格，REST 服务，关系型[数据库](http://severalnines.com/blog/archival-and-analytics-importing-mysql-data-hadoop-cluster-using-sqoop)等。

～ 作者 mdavey，2016 年 4 月 24 日发布。

发表在 [数据](https://mdavey.wordpress.com/category/data/) 中。

标签: [数据湖](https://mdavey.wordpress.com/tag/datalake/), [机器学习](https://mdavey.wordpress.com/tag/machinelearning/)
