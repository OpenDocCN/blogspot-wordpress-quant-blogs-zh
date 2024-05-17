<!--yml
category: 未分类
date: 2024-05-18 05:33:16
-->

# Machine Learning: Spark vs Flink | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/04/26/machine-learning-spark-vs-flink/#0001-01-01](https://mdavey.wordpress.com/2016/04/26/machine-learning-spark-vs-flink/#0001-01-01)

## Machine Learning: Spark vs Flink

Interesting slide deck from Capital One [comparing](http://www.slideshare.net/sbaltagi/flink-vs-spark) Flink vs Spark.  H2O has Spark integration though [SparkingWater](http://www.h2o.ai/product/sparkling-water/) which is all well and good, but Flink look more interesting 🙂

Having not done much work with [TensorFlow](https://www.tensorflow.org/), I see it has its own cluster for [distribution](https://www.tensorflow.org/versions/r0.8/how_tos/distributed/index.html#distributed-tensorflow).  However, [databricks](https://databricks.com/blog/2016/01/25/deep-learning-with-spark-and-tensorflow.html) has integrated it with [Spark](https://www.infoq.com/news/2016/03/databricks-spark-tensorflow).

[Deeplearning4j](http://deeplearning4j.org/) provide a interesting [comparison](http://deeplearning4j.org/compare-dl4j-torch7-pylearn.html) of a number of ML libraries, with mention of Spark, but no mention of Flink.

There is some benchmarking of Spark and Flink [here](http://sparkbigdata.com/102-spark-blog-slim-baltagi/14-results-of-a-benchmark-between-apache-flink-and-apache-spark), with in many ways expected outcomes:

> Apache Flink outperforms Apache Spark in processing machine learning & graph algorithms and relational queries but not in batch processing!

Some searching, and we get to [Full Metal](http://bigstep.com/full-metal-data-lake) Data Lake.  Interesting, but not quite what I’m looking for.  However, it does point me at Apache [Drill](https://drill.apache.org/).

“Data Lake Architecture [Considerations](http://dataottam.com/2016/02/13/data-lake-architecture-considerations-composition/) & Composition” provides direction on a Data Lake architecture being composed of three layers and three tiers.  Extremely helpful, and one of the better articles I’ve found on data lakes.  Probably also worth a [read](http://dataottam.com/2016/03/26/2nd-version-of-data-lake-vs-data-warehouse/) is “2nd Version of Data Lake vs. Data Warehouse”

Back to Flink, Zalando’s next generation data integration and distribution platform Saiki provides some thoughts on [architecture](https://tech.zalando.com/blog/apache-showdown-flink-vs.-spark/).  Nice to see Saiki’s unified log uses Apache Kafka to feed the data lake – great choice 🙂

~ by mdavey on April 26, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/), [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)
Tags: [ApacheFlink](https://mdavey.wordpress.com/tag/apacheflink/), [BigData](https://mdavey.wordpress.com/tag/bigdata/), [DataLake](https://mdavey.wordpress.com/tag/datalake/), [MachineLearning](https://mdavey.wordpress.com/tag/machinelearning/)