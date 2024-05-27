<!--yml

类别：未分类

日期：2024-05-18 05:50:01

-->

# 统一/自由 Lambda 架构 | 交易桌旁的传说

> 来源：[`mdavey.wordpress.com/2014/05/16/unified-free-lambda-architectures-2/#0001-01-01`](https://mdavey.wordpress.com/2014/05/16/unified-free-lambda-architectures-2/#0001-01-01)

## 统一/自由 Lambda 架构

最近一直在思考[lambda](http://www.meetup.com/Accumulo-Users-DC/events/178839102/)架构。[Datasalt](http://www.datasalt.com/2014/01/lambda-architecture-a-state-of-the-art/)几个月前提供了一个更新，指向了统一和自由 Lambda 架构：

+   统一 – 实时层和批处理层都有相同的代码，并且透明地合并两层的结果

+   自由 – 每个层次独立运作，根据业务性质合并结果

文章还参考了 VoltDB 与 Hadoop 一起使用的[有趣用法](http://www.youtube.com/watch?v=VVmSR--Yt5E&feature=youtu.be)。

[Summingbird](https://speakerdeck.com/sritchie/summingbird-streaming-mapreduce-at-twitter)和[lambdoop](http://www.slideshare.net/Datadopter/lambdoop-a-framework-for-easy-development-of-big-data-applications)看起来[很有趣](http://www.slideshare.net/tantrieuf31/reactive-realime-big-data-techcampvn-2014)。

MapR 提供了关于[lambda](http://www.mapr.com/developercentral/lambda-architecture)架构的进一步[思考](http://www.mapr.com/developercentral/lambda-architecture)。InfoQ 也有一篇有趣的[文章](http://www.infoq.com/articles/lambda-architecture-scalable-big-data-solutions)关于可扩展的大数据解决方案。

~ by mdavey on May 16, 2014.

发表于[云](https://mdavey.wordpress.com/category/hpc/cloud/)
