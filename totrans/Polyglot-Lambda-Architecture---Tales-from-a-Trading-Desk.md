<!--yml
category: 未分类
date: 2024-05-18 05:41:12
-->

# Polyglot Lambda Architecture | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2015/06/29/polyglot-lambda-architecture/#0001-01-01](https://mdavey.wordpress.com/2015/06/29/polyglot-lambda-architecture/#0001-01-01)

## Polyglot Lambda Architecture

[OTTO](http://dev.otto.de/) has a number of great postings on the work they are doing.  One of the most recent [articles](http://dev.otto.de/2015/06/23/a-tale-of-two-lambdas-2/) is “A tale of two [lambdas](http://www.slideshare.net/helenaedelson/lambda-architecture-with-spark-spark-streaming-kafka-cassandra-akka-and-scala): The joys of working in a polyglot team.” which speaks volumes to using the right language for the problem you are trying to solve.  Spark has really helped to move the [lambda](http://blog.cloudera.com/blog/2014/08/building-lambda-architecture-with-spark-streaming/) concept forwards in the last time period.  Would also agree with OTT on  Elasticsearch – [ELK](https://www.elastic.co/products).  Personally not used [Graphite](http://graphite.wikidot.com/screen-shots), but it does look interesting.

On MLlib, I’ve previously blogged about success with trading research/idea recommendations.  Its also worth calling out that [Logisitic](https://spark.apache.org/docs/latest/mllib-linear-methods.html#logistic-regression) Regression algorithm is very useful in finding relationship from binary response variables – an example in the trading world is the age old classic RFQ reject/accept.

~ by mdavey on June 29, 2015.

Posted in [Languages](https://mdavey.wordpress.com/category/languages/)