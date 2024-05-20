<!--yml
category: 未分类
date: 2024-05-18 05:56:36
-->

# In-Stream Big Data Query Processing Pipeline: Storm, Cassandra, Kafka | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/12/11/in-stream-big-data-query-processing-pipeline-storm-cassandra-kafka/#0001-01-01](https://mdavey.wordpress.com/2013/12/11/in-stream-big-data-query-processing-pipeline-storm-cassandra-kafka/#0001-01-01)

## In-Stream Big Data Query Processing Pipeline: Storm, Cassandra, Kafka

Interesting [read](http://highlyscalable.wordpress.com/2013/08/20/in-stream-big-data-processing/) on the shortcomings and drawbacks of batch-oriented data processing over on Highly Scalable.  Data partitioning and shuffling are discussed as solutions to large data sets.  Lineage tracking is also discussed 🙂 The article concludes with a brief overview of the solution built with Storm, Cassandra and Kafka:

> The system naturally uses Kafka 0.8 as a partitioned fault-tolerant event buffer to enable stream replay and improve system extensibility by easy addition of new event producers and consumers. Kafka’s ability to rewind read pointers also enables random access to the incoming batches and, consequently, Spark-style lineage tracking. It is also possible to point the system input to HDFS to process the historical data.
> 
> Cassandra is employed for state checkpointing and in-store aggregation, as described earlier. In many use cases, it also stores the final results.
> 
> Twitter’s Storm is a backbone of the system. All active query processing is performed in Storm’s topologies that interact with Kafka and Cassandra. Some data flows are simple and straightforward: the data arrives to Kafka; Storm reads and processes it and persist the results to Cassandra or other destination. Other flows are more sophisticated: one Storm topology can pass the data to another topology via Kafka or Cassandra.

In the move towards unified big data processing, as pointed out in the article, Apache [Spark](one%20Storm%20topology%20can%20pass%20the%20data%20to%20another%20topology%20via%20Kafka%20or%20Cassandra.) is of interest – streaming sample [here](https://github.com/apache/incubator-spark/tree/master/examples/src/main/java/org/apache/spark/streaming/examples).

~ by mdavey on December 11, 2013.

Posted in [Data](https://mdavey.wordpress.com/category/data/)