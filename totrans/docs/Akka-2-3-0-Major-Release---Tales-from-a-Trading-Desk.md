<!--yml
category: 未分类
date: 2024-05-18 05:53:00
-->

# Akka 2.3.0 Major Release | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2014/03/05/akka-2-3-0-major-release/#0001-01-01](https://mdavey.wordpress.com/2014/03/05/akka-2-3-0-major-release/#0001-01-01)

## Akka 2.3.0 Major Release

Great to see the next version of Akka [released](http://typesafe.com/blog/akka-230-major-release) that includes the following [key](http://typesafe.com/blog/akka-230-major-release) features:

*   Akka Persistence
*   Java 8 support
*   Cluster improvements
*   Activator Templates

Cool take aways:

> Akka Persistence also supports event sourcing
> 
> We have something brewing which will be more than just a replacement for Pipelines: inspired by RxJava we are working on implementing Reactive Streams for Akka which will allow declarative transformation of streaming data of all kinds, with proper handling of back-pressure and of course fully typed.
> 
> [Sharding of actors](http://doc.akka.io/docs/akka/2.3.0/contrib/cluster-sharding.html) in a cluster. The typical use case for this feature is when you have many stateful actors that together consume more resources (e.g. memory) than fit on one machine. You need to distribute them across several nodes in the cluster and you want to be able to interact with them using their logical identifier, but without having to care about their physical location in the cluster, which might also change over time. It could for example be actors representing Aggregate Roots in Domain-Driven Design terminology.

As blogged about before, the activator templates are brilliant for quick starts to projects.  Akka persistence is welcomed.

~ by mdavey on March 5, 2014.

Posted in [Languages](https://mdavey.wordpress.com/category/languages/)
Tags: [akka](https://mdavey.wordpress.com/tag/akka/)