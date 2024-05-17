<!--yml
category: 未分类
date: 2024-05-18 05:33:37
-->

# Data Lake Architecture: Stream Centric | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/04/26/data-lake-architecture-stream-centric/#0001-01-01](https://mdavey.wordpress.com/2016/04/26/data-lake-architecture-stream-centric/#0001-01-01)

## Data Lake Architecture: Stream Centric

There are numerous mays to create and feed your data lake.  One theme that is particularly interesting leverages Apache Kafka, and is well documented in “Putting Apache Kafka To Use: A Practical Guide to Building a Stream Data [Platform](http://www.confluent.io/blog/stream-data-platform-1/)“.  The article does a good job of explaining the ad-hoc road:

> “piping between systems and applications on an as needed basis and shoe-horned any asynchronous processing into request-response web services. “

Which turns into an interesting [diagram](http://cdn2.hubspot.net/hub/540072/file-3062870508-png/blog-files/data-flow-ugly.png) 🙂

The article then goes onto Version 2, appropriately names “Kafka stuff” which has an improved [architecture](http://cdn2.hubspot.net/hub/540072/file-3062870518-png/blog-files/stream_data_platform.png), with well defined flows and patterns – “stream-centric data architecture”, and benefits:

1.  > **Data Integration**: The stream data platform captures streams of events or data changes and feeds these to other data systems such as relational databases, key-value stores, Hadoop, or the data warehouse.

2.  > **Stream processing**: It enables continuous, real-time processing and transformation of these streams and makes the results available system-wide.

In the case of leveraging [H2O](http://www.h2o.ai/), this offer the ability to leverage Flow through SparkingWater on top of Apache Spark and the Data Lake (HDFS), and also off Apache Kafka streaming using the H2O POJO’s, opening up the opportunity for real-time pushed business insight to the User Experience.

[Both](http://www.confluent.io/blog/stream-data-platform-1/) [articles](http://www.confluent.io/blog/stream-data-platform-2/) are well worth a read.

Curious if any readers have found an improved approach over Apache Kafka to solve the Data [Lake](http://searchbusinessanalytics.techtarget.com/feature/Building-a-data-lake-architecture-can-drag-unprepared-users-under) data integration problem, and likewise the Machine Learning solution.

~ by mdavey on April 26, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
Tags: [DataLake](https://mdavey.wordpress.com/tag/datalake/), [MachineLearning](https://mdavey.wordpress.com/tag/machinelearning/)