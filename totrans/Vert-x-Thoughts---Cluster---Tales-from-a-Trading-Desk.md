<!--yml
category: 未分类
date: 2024-05-18 05:55:31
-->

# Vert.x Thoughts – Cluster | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2014/01/03/vert-x-thoughts-cluster/#0001-01-01](https://mdavey.wordpress.com/2014/01/03/vert-x-thoughts-cluster/#0001-01-01)

## Vert.x Thoughts – Cluster

Lance’s “Async Data From Cluster to Browser” [presentation](http://lanceball.com/dataIO2013/#/) provided in my view the golden nugget of information on slide [2](http://lanceball.com/dataIO2013/#/1), “application platform”.  If you haven’t played with Vertx yet, then I suggest you download and [install](http://vertx.io/install.html).  As discussed before on this blog, [reactive](http://vertx.io/manual.html#asynchronous-programming-model) is “interesting”.    If you’ve played with Akka, and the Actor pattern, you maybe interested in [Vertx](http://www.slideshare.net/wuman/development-with-vertx-an-eventdriven-application-framework-for-the-jvm) when you read the Vertx manual on event bus, and [HA](http://vertx.io/manual.html#high-availability-with-vertx)/cluster features.  A distributed event bus, over a cluster of reactive Module/*verticles*.

> Simple *actor-like* concurrency model. [Vert.x](http://www.cubrid.org/blog/dev-platform/understanding-vertx-architecture-part-2/) allows you to write all your code as single threaded, freeing you from many of the pitfalls of multi-threaded programming. (No more `synchronized`, `volatile` or explicit locking).

A few [Vert.x](http://parleys.com/play/5148922b0364bc17fc56c8c7/chapter0/about) samples are available [here](https://github.com/vert-x/vertx-examples).  Work queue module available [here](https://github.com/vert-x/mod-work-queue).  Mongo persistor [here](https://github.com/vert-x/mod-mongo-persistor).

~ by mdavey on January 3, 2014.

Posted in [Languages](https://mdavey.wordpress.com/category/languages/)
Tags: [Vertx](https://mdavey.wordpress.com/tag/vertx/)