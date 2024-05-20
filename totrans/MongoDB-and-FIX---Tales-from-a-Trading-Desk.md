<!--yml
category: 未分类
date: 2024-05-18 06:22:37
-->

# MongoDB and FIX | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/07/12/mongodb-and-fix/#0001-01-01](https://mdavey.wordpress.com/2013/07/12/mongodb-and-fix/#0001-01-01)

## MongoDB and FIX

Interesting [Webinar](http://www.slideshare.net/mongodb/webinar-processing-high-volume-data-feeds-with-mongodb-fix-fpml-and-swift-in-association-with-c24) from C24 around feeding [MongoDB](http://www.c24.biz/c24-io-financial-messaging-mongodb-integration.html) with FIX messages.  Curious if anyone is using this in production today.  The MongoDB [aggregation](http://docs.mongodb.org/manual/core/aggregation/) framework can probably full together some nice data once the FIX messages are in MongoDB e.g. the all FIX message for RFQ @time x etc.  Matt’s blog [posting](http://techiquest.blogspot.co.uk/2012/09/c24-and-mongodb-agile-message.html) provides an ExecutionReport sample using C24 code, but unfortunately doesn’t go into the aggregation uses of FIX message once the ExecutionReport’s are in MongoDB

~ by mdavey on July 12, 2013.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)
Tags: [MongoDB](https://mdavey.wordpress.com/tag/mongodb/), [NoSQL](https://mdavey.wordpress.com/tag/nosql/)