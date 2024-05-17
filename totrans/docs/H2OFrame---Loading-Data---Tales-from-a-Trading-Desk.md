<!--yml
category: 未分类
date: 2024-05-18 05:33:20
-->

# H2OFrame – Loading Data | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/04/20/h2oframe-loading-data/#0001-01-01](https://mdavey.wordpress.com/2016/04/20/h2oframe-loading-data/#0001-01-01)

## H2OFrame – Loading Data

“Apache [Spark](http://spark.apache.org/) is a fast and general engine for large-scale data processing”.  Clearly this is the reason H2O has been married to Spark through [Sparkling](http://www.h2o.ai/product/sparkling-water/) Water.  This [integration](https://github.com/h2oai/sparkling-water) offers:

> *   Utilities to publish Spark data structures (RDDs, DataFrames) as H2O’s frames and vice versa
> *   DSL to use Spark data structures as input for H2O’s algorithms
> *   Basic building blocks to create ML applications utilizing Spark and H2O APIs
> *   Python interface enabling use of Sparkling Water directly from pySpark

“How-to: Build a Machine-Learning App Using Sparkling Water and Apache Spark” provides insight into the conversation of data between Spark and H2O – from Spark resilient distributed dataset (RDD)  to H2OFrame and vice versa.

H2OFrame offers a few other ways to load data into H2OFrame’s as provided by [this](http://h2o-release.s3.amazonaws.com/h2o/master/3384/docs-website/h2o-docs/booklets/SparklingWaterVignette.pdf) documentation page:

> *   local filesystems
> *   HDFS
> *   S3
> *   HTTP/HTTPS

I’m therefore wondering, if the data set is relatively small, its probably easier to expose the data through a REST endpoint rather than downloading to CVS just to load the file into H2OFrame.  Maybe in the scenario were at the end of a time period, I want a snap of data?  I can see the advantage of SparklingWater when I’ve got data in hdfs or I need the Spark cluster power on a particular problem.  However, for small datasets, I’m not sure one needs SparklingWater ?

Which leads to the following thought process:

*   If your streaming data, then decide where the POJO model is going to run – its Java, so this should be easy – data subscriber.
*   If you are have lots of data, SparklingWater and cluster is needed to ensure performance
*   If your spiking, RStudio of similar for accessing H2O is good enough
*   Hooking in streaming data to Apache Spark and H2O doesn’t seem to be required, given the first bullet point above.

~ by mdavey on April 20, 2016.

Posted in [Agile](https://mdavey.wordpress.com/category/agile/)
Tags: [MachineLearning](https://mdavey.wordpress.com/tag/machinelearning/)