<!--yml

category: 未分类

date: 2024-05-18 06:22:37

-->

# MongoDB 和 FIX | 交易桌旁的故事

> 来源：[`mdavey.wordpress.com/2013/07/12/mongodb-and-fix/#0001-01-01`](https://mdavey.wordpress.com/2013/07/12/mongodb-and-fix/#0001-01-01)

## MongoDB and FIX

来自 C24 的一个有趣的[网络研讨会](http://www.slideshare.net/mongodb/webinar-processing-high-volume-data-feeds-with-mongodb-fix-fpml-and-swift-in-association-with-c24)，讨论如何用 FIX 消息喂养 [MongoDB](http://www.c24.biz/c24-io-financial-messaging-mongodb-integration.html)。很好奇现在是否有人正在生产环境中使用它。一旦 FIX 消息存储在 MongoDB 中，MongoDB [聚合](http://docs.mongodb.org/manual/core/aggregation/)框架可能能够组装一些很棒的数据，例如在时间 x 处的所有 FIX 消息请求（RFQ）等。Matt 的博客[帖子](http://techiquest.blogspot.co.uk/2012/09/c24-and-mongodb-agile-message.html)提供了一个使用 C24 代码的 ExecutionReport 示例，但不幸的是，它没有深入讨论一旦 ExecutionReport 存储在 MongoDB 中，FIX 消息的聚合使用情况。

~ by mdavey on July 12, 2013.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)

Tags: [MongoDB](https://mdavey.wordpress.com/tag/mongodb/), [NoSQL](https://mdavey.wordpress.com/tag/nosql/)
