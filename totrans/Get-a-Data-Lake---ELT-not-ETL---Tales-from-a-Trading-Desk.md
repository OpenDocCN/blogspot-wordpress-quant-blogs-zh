<!--yml
category: 未分类
date: 2024-05-18 05:33:24
-->

# Get a Data Lake – ELT not ETL | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/04/24/get-a-data-lake-elt-not-etl/#0001-01-01](https://mdavey.wordpress.com/2016/04/24/get-a-data-lake-elt-not-etl/#0001-01-01)

## Get a Data Lake – ELT not ETL

[Data Lakes](http://www.blue-granite.com/blog/bid/402596/Top-Five-Differences-between-Data-Lakes-and-Data-Warehouses) are one of the buzzwords that has been going around for some time in the “big data” era.  Many [companies](https://spark-summit.org/2015/events/a-big-data-lake-based-on-spark-for-bbva-bank/)/people has figures out what a data lake is, have create one, and are using it to great effect.  Others are still [confused](http://www.snowflake.net/blog/data-lake-or-data-swamp/) or unsure.

There are many articles and blog posts these days which provide clarity on data lakes.  Here’s [one](http://www.infoq.com/articles/cazena-big-data-as-a-service) definition:

> A Data Lake is a data store used for storing and processing large volumes of data. They are often used to collect raw data in native format before datasets are used for analytics purposes

Which leads to, in many ways, a pivotal line, “ELT not ETL” – thanks to James Serra’s [posting](http://www.jamesserra.com/archive/2015/04/what-is-a-data-lake/).

> ELT instead of ETL (loading the data into the data lake and then processing it). This can speed up transformations as the data lake is usually in a Hadoop cluster that can transform data much faster than an ETL tool

Which then leads to identification of all the data sources in your organisation, a deciding how best to extract and load the data from those sources – SpreadSheets, REST services, relational [databases](http://severalnines.com/blog/archival-and-analytics-importing-mysql-data-hadoop-cluster-using-sqoop), etc.

~ by mdavey on April 24, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
Tags: [DataLake](https://mdavey.wordpress.com/tag/datalake/), [MachineLearning](https://mdavey.wordpress.com/tag/machinelearning/)