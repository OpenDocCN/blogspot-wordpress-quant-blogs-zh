<!--yml
category: 未分类
date: 2024-05-18 05:33:07
-->

# Machine Learning on Streaming Data – Samza and Flink | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/04/28/machine-learning-on-streaming-data-samza-and-flink/#0001-01-01](https://mdavey.wordpress.com/2016/04/28/machine-learning-on-streaming-data-samza-and-flink/#0001-01-01)

## Machine Learning on Streaming Data – Samza and Flink

Based on a few comments, coupled with various web reading, I get the impression Spark and Storm are not the latest solution to use in a Streaming Data Machine Learning platform – maybe I’m wrong?  Apache [Samza](http://samza.apache.org/) and [Flink](http://flink.apache.org/) appear to be the new kids on the block.  There are a few comparisons of the various streaming engines – one [here](http://www.altaterra.net/blogpost/288668/225612/Which-Stream-Processing-Engine-Storm-Spark-Samza-or-Flink), and another [here](http://www.cakesolutions.net/teamblogs/comparison-of-apache-stream-processing-frameworks-part-1).

Samza is very interesting, since it uses a technology I like a lot, Apache Kafka 🙂  Flink however appears to be the newest kid on the block 🙂 , and based on this simple code [comparison](http://www.cakesolutions.net/teamblogs/comparison-of-apache-stream-processing-frameworks-part-1), offers a clean API.

dataArtisans “Kafka + Flink: A [practical](http://data-artisans.com/kafka-flink-a-practical-how-to/), how-to guide” article offer some direction on connecting Kafka and Flink, which in many ways might be the approach to take to running Machine Learning models against streaming data.

Finally, although old, “Apache Flink: API, runtime, and project [roadmap](http://www.slideshare.net/KostasTzoumas/apache-flink-api-runtime-and-project-roadmap)” slide 62 provide a view of the roadmap for Flink to integrate with Machine Learning libraries – also slide 67, with H2O mentioned on slide 71.

The next bus: Apache [Kudu](http://getkudu.io/)?

~ by mdavey on April 28, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
Tags: [MachineLearning](https://mdavey.wordpress.com/tag/machinelearning/), [StreamingData](https://mdavey.wordpress.com/tag/streamingdata/)