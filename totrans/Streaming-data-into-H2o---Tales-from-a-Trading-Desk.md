<!--yml
category: 未分类
date: 2024-05-18 05:33:46
-->

# Streaming data into H2o | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/04/20/streaming-data-into-h2o/#0001-01-01](https://mdavey.wordpress.com/2016/04/20/streaming-data-into-h2o/#0001-01-01)

## Streaming data into H2o

Not something that appears widely publicised, which in my view is strange given the real-time world we live in these days, but after some web searching I found a relevant article on the H2O World 2015 Training [site](http://learn.h2o.ai/content/tutorials/streaming/storm/index.html).

*   databrick [streaming](https://databricks.com/blog/category/engineering/streaming)
*   Diving into Spark Streaming’s [Execution](https://databricks.com/blog/2015/07/30/diving-into-spark-streamings-execution-model.html) Model
*   Improvements to Kafka [integration](https://databricks.com/blog/2015/03/30/improvements-to-kafka-integration-of-spark-streaming.html) of Spark Streaming
*   How-to: Build a Machine-Learning App Using Sparkling Water and Apache [Spark](http://blog.cloudera.com/blog/2015/10/how-to-build-a-machine-learning-app-using-sparkling-water-and-apache-spark/)

Real-time Predictions With H2O on [Storm](http://learn.h2o.ai/content/tutorials/streaming/storm/index.html) isn’t quite what I was looking for, I’m more interested in Apache Kafka.  However, its close enough to the problem to be useful 🙂

Source code can be found [here](https://github.com/h2oai/h2o-tutorials/tree/master/tutorials/streaming/storm). TestH2ODataSpout.java is the fake real-time data.  [H2OStormStarter.java](https://github.com/h2oai/h2o-tutorials/blob/master/tutorials/streaming/storm/H2OStormStarter.java) is the interesting code, which consumes the real-time data, and pushing results out via the collector emit() and ack() functions.

PredictionBolt emits tuples via the collector to ClassifierBolt who write the data to a file (out) and also emits the classification result to the collector.

The cheat is that ClassifierBolt write to a file (out), which is read by the JS code.  In reality the results from ClassifierBolt should probably go via a websocket to the HTML user interface.

Net out, using Storm, Kafka or other technology is irrelevant, the key is exporting the model as a Java POJO via R, and h2o.download_pojo().

~ by mdavey on April 20, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
Tags: [H2O](https://mdavey.wordpress.com/tag/h2o/), [Kafka](https://mdavey.wordpress.com/tag/kafka/), [MachineLearning](https://mdavey.wordpress.com/tag/machinelearning/)