```yml

分类：未分类

日期：2024-05-18 05:31:38

→

# Spark SQL：统一数据访问 | 交易桌旁的点滴

> 来源：[`mdavey.wordpress.com/2016/06/02/spark-sql-unified-data-access/#0001-01-01`](https://mdavey.wordpress.com/2016/06/02/spark-sql-unified-data-access/#0001-01-01)

## Spark SQL：统一数据访问

[Spark](http://spark.apache.org/)近年来势头强劲。当与[H2O](http://www.h2o.ai/product/sparkling-water/)结合时，在商业转型的 AI 世界中提供了相当大的力量。Spark 的一个好处是能够以一致的方式访问各种数据源——数据框/[Spark SQL](https://databricks.com/blog/2015/01/09/spark-sql-data-sources-api-unified-data-access-for-the-spark-platform.html)。在支持的其他数据源中，[JDBC](http://spark.apache.org/docs/latest/sql-programming-guide.html#data-sources)和 Hive 得到了支持。完整的 Spark 数据源包列表可以在[这里](https://spark-packages.org/?q=tags%3A%22Data%20Sources%22)找到。[CSV](https://spark-packages.org/package/databricks/spark-csv)文件甚至得到支持：）

我以为会支持的一个数据源是 JIRA，但看起来并不支持。JSON 数据文件是 Spark 支持的，但从 REST 端点检索 JSON（这可能是与 JIRA 配合使用的最佳方式）似乎并不支持。

**更新**： “Spark Summit EU 2015：Spark DataFrames：对结构化数据的简单快速分析”的第 16 张幻灯片有一个加载 JIRA 数据并将其存储在 Hive 中的示例。

~ mdavey 于 2016 年 6 月 2 日。

发布于[数据](https://mdavey.wordpress.com/category/data/)分类

标签：[Spark](https://mdavey.wordpress.com/tag/spark/)
