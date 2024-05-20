<!--yml
category: 未分类
date: 2024-05-18 06:36:31
-->

# More Thoughts Around Apache Kafka – FIX Logs | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2012/08/08/more-thoughts-around-apache-kafka-fix-logs/#0001-01-01](https://mdavey.wordpress.com/2012/08/08/more-thoughts-around-apache-kafka-fix-logs/#0001-01-01)

## More Thoughts Around Apache Kafka – FIX Logs

Earlier this year I blogged about Raptor (Sungard) and real-time analytics.  This posting follow on with a few specific Kafka thoughts:

*   Kafka’s [design](http://incubator.apache.org/kafka/design.html) page provides a few use cases, around “activity streams”.  Of interesting is the list of companies [mentioned](https://cwiki.apache.org/confluence/display/KAFKA/Powered+By) that are using Kafka – in particular [Metamarkets](http://metamx.com/), a company I have blogged about before in the big data analysis space.
*   The reference to log files is of particular interest:

> Activity stream data is a normal part of any website for reporting on usage of the site. Activity data is things like page views, information about what content was shown, searches, etc. This kind of thing is usually handled by logging the activity out to some kind of file and then periodically aggregating these files for analysis

*   The above lead to the thoughts around FIX messages, and specific the type of product that are commercially available from various vendors e.g. B2BITS with its [FIX](http://qwtradingsystem.com/documents/QWFIX/main/Getting%20Started/Features%20Tour/QWFIX%20RTAnalyzer/1.FIXMessageMonitoring.htm) log [analyzers](http://www.b2bits.com/trading_solutions/fix_log_analyzers.html)
*   OnixS FIX Analyser is again similar, monitoring log [files](http://www.onixs.biz/fix-analyser.html)
*   All the above leads to leveraging Kafka to process FIX log files in real-time.
*   The Log4j [appender](http://incubator.apache.org/kafka/quickstart.html) as show here should make things easy from an application perspective
*   Likewise the Hadoop [consumer](https://github.com/kafka-dev/kafka/tree/master/contrib/hadoop-consumer) offers some interesting possibilities

Further, assuming you now have this data, it maybe interesting to “count” FIX messages, which [possibly](http://www.slideshare.net/dave_revell/nearrealtime-analytics-with-kafka-and-hbase#) leads us to [data cube](https://github.com/urbanairship/datacube) (backed by HBase).
[Storm](http://www.slideshare.net/Hadoop_Summit/realtime-analytics-with-storm) also offer interesting [possibilities](https://github.com/nathanmarz/storm/wiki/Kestrel-and-Storm) with FIX messages – another posting.

~ by mdavey on August 8, 2012.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)
Tags: [Messaging](https://mdavey.wordpress.com/tag/messaging/)