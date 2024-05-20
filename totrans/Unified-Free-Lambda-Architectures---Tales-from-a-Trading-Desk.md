<!--yml
category: 未分类
date: 2024-05-18 05:50:01
-->

# Unified/Free Lambda Architectures | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2014/05/16/unified-free-lambda-architectures-2/#0001-01-01](https://mdavey.wordpress.com/2014/05/16/unified-free-lambda-architectures-2/#0001-01-01)

## Unified/Free Lambda Architectures

Been pondering about [lambda](http://www.meetup.com/Accumulo-Users-DC/events/178839102/) architectures recently.  [Datasalt](http://www.datasalt.com/2014/01/lambda-architecture-a-state-of-the-art/) offers an update a few months ago, pointing us at unified and free lambda architectures:

*   Unified – the same code available to both the real-time and batch layer, and combines the results of both layers transparently
*   Free – each layer operates independently and results are merged depending on the business nature

The article also references an interesting [usage](http://www.youtube.com/watch?v=VVmSR--Yt5E&feature=youtu.be) of VoltDB with Hadoop.

[Summingbird](https://speakerdeck.com/sritchie/summingbird-streaming-mapreduce-at-twitter) and [lambdoop](http://www.slideshare.net/Datadopter/lambdoop-a-framework-for-easy-development-of-big-data-applications) look [interesting](http://www.slideshare.net/tantrieuf31/reactive-realime-big-data-techcampvn-2014).

MapR offers further [thoughts](http://www.mapr.com/developercentral/lambda-architecture) on [lambda](http://spark-summit.org/2014/talk/applying-the-lambda-architecture-with-spark) architectures.  InfoQ also has an interesting [article](http://www.infoq.com/articles/lambda-architecture-scalable-big-data-solutions).

~ by mdavey on May 16, 2014.

Posted in [Cloud](https://mdavey.wordpress.com/category/hpc/cloud/)