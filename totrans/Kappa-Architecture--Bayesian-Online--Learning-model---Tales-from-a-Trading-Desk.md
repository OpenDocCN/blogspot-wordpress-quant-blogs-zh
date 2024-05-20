<!--yml
category: 未分类
date: 2024-05-18 05:31:17
-->

# Kappa Architecture: Bayesian Online-­Learning model | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/06/08/kappa-architecture-bayesian-online-%c2%adlearning-model/#0001-01-01](https://mdavey.wordpress.com/2016/06/08/kappa-architecture-bayesian-online-%c2%adlearning-model/#0001-01-01)

## Kappa Architecture: Bayesian Online-­Learning model

“Applying the Kappa [architecture](https://www.oreilly.com/ideas/applying-the-kappa-architecture-in-the-telco-industry) in the telco industry” from  Strata + Hadoop World London 2016 offers a great read.  A large number of companies don’t really have a data volume problem, but they do have the “shorter time constraints, and an increasing need for accuracy” to derive business transformation though the use of AI.

The first statement that stands out from this article is:

> Bayesian online-­learning model to detect novelties

There are so many use cases that customer and employee data sets from a corporations standpoint that could benefit from novelty detection.

The Kappa architecture is a nice twist on the lambda architecture that I’ve blogged about previous.  Streaming is the only way these days, especially with the evolution of Apache Spark Streaming – “batch processing is a subset of stream processing.”

“Immutable data sources” and raw data relates nicely to the [ELT](https://en.wikipedia.org/wiki/Extract,_load,_transform) view of the world blogged about elsewhere over the last time period

The article unfortunately doesn’t say which ML library was used for the Bayesian anomaly detector 😦

Interesting to see that Apache [Flink](https://flink.apache.org/) was used and not Apache [Spark](http://spark.apache.org/).  Nice to see Apache [Kafka](http://kafka.apache.org/) as the data conduit 🙂

~ by mdavey on June 8, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
Tags: [Kappa](https://mdavey.wordpress.com/tag/kappa/), [MachineLearning](https://mdavey.wordpress.com/tag/machinelearning/)