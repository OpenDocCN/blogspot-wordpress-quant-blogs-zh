<!--yml
category: 未分类
date: 2024-05-18 05:31:38
-->

# Spark SQL: Unified Data Access | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/06/02/spark-sql-unified-data-access/#0001-01-01](https://mdavey.wordpress.com/2016/06/02/spark-sql-unified-data-access/#0001-01-01)

## Spark SQL: Unified Data Access

[Spark](http://spark.apache.org/) has gained in momentum over the years.   When married to [H2O](http://www.h2o.ai/product/sparkling-water/), it offer considerable power in the AI world of business transformation.  One nice feature of Spark is the ability to access various data sources in a consistent way – data frames/[Spark SQL](https://databricks.com/blog/2015/01/09/spark-sql-data-sources-api-unified-data-access-for-the-spark-platform.html).  Amongst other data sources, [JDBC](http://spark.apache.org/docs/latest/sql-programming-guide.html#data-sources) and Hive are supported.  A fuller list of Spark Data Source packages is available [here](https://spark-packages.org/?q=tags%3A%22Data%20Sources%22).  [CSV](https://spark-packages.org/package/databricks/spark-csv) files are even supported 🙂

One data source that I thought would be supported, but doesn’t seem to be, is JIRA.  JSON data files are supported by Spark, but support to retrieve JSON from a REST endpoint (which is probably the way to go with JIRA) doesn’t seem to be supported out the box.

**Update**:  “Spark Summit EU 2015: Spark DataFrames: Simple and Fast Analysis of Structured Data” slide 16 has an example of loading JIRA data and storing it in Hive.

~ by mdavey on June 2, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
Tags: [Spark](https://mdavey.wordpress.com/tag/spark/)