<!--yml
category: 未分类
date: 2024-05-18 05:35:45
-->

# Feeding a Data Refinery with Kafka | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/03/11/feeding-a-data-refinery-with-kafka/#0001-01-01](https://mdavey.wordpress.com/2016/03/11/feeding-a-data-refinery-with-kafka/#0001-01-01)

## Feeding a Data Refinery with Kafka

Following on from an earlier posting on [Data Refineries](https://mdavey.wordpress.com/2016/01/21/real-time-data-refinery/), I’m now beginning to consider connecting [Kafka](http://kafka.apache.org/) (my distributed commit-log) to H2O.  [H2O](http://www.h2o.ai/) looks interested based on using R-Studio for a short while, couple with the availability of [analytics](http://hortonworks.com/hadoop-tutorial/predictive-analytics-h2o-hortonworks-data-platform/), and the general uptake of the platform – am I wrong?

I can’t find a lot using Google around connecting Kafka to H2O.  Hence I’m wondering if I should look to the road of connecting Kafka to Spark, and thus use [Sparking Water](http://www.h2o.ai/product/sparkling-water/)?  Spark offers a few options for [connecting](http://spark.apache.org/docs/latest/streaming-kafka-integration.html) to Kafka:

1.  Receiver-based Approach
2.  Direct Approach (No Receivers)

The No Receivers approach appears to be the preferred road, with the benefit of zero data loss – always a good thing 🙂

Taking this a step further, I wonder what predictions are achievable if I took the skill cloud, married with other interesting “data” as per the Cloud Skill [postings](https://mdavey.wordpress.com/2014/06/03/skill-cloud-part-3/).

~ by mdavey on March 11, 2016.

Posted in [Cloud](https://mdavey.wordpress.com/category/hpc/cloud/), [Data](https://mdavey.wordpress.com/category/data/), [Java](https://mdavey.wordpress.com/category/languages/java/), [Languages](https://mdavey.wordpress.com/category/languages/)