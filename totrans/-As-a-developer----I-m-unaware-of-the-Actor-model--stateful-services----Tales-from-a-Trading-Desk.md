<!--yml
category: 未分类
date: 2024-05-18 05:38:34
-->

# “As a developer..” I’m unaware of the Actor model (stateful services) | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2015/10/28/as-a-developer-im-unaware-of-the-actor-model-stateful-services/#0001-01-01](https://mdavey.wordpress.com/2015/10/28/as-a-developer-im-unaware-of-the-actor-model-stateful-services/#0001-01-01)

## “As a developer..” I’m unaware of the Actor model (stateful services)

Almost every day there is another “micro services” article that implies the new silver bullet to software architecture will solve all current architecture problems.  Its therefore refreshing to [read](http://highscalability.com/blog/2015/10/12/making-the-case-for-building-scalable-stateful-services-in-t.html) “Making The Case For Building Scalable Stateful Services In The Modern Era”.  What’s also interesting is Caitie McCaffrey “Building Scalable Stateful Services” [presentation](https://speakerdeck.com/caitiem20/building-scalable-stateful-services) due to the many patterns discussed – Sticky Sessions, Data Shipping Paradigm, Function Shipping Paradigm, Data Locality, CAP, Cluster Membership, Gossip Protocols, Consistent Hashing, DHT.  There is also a nice mention of Microsofts Orleans runtime and programming model based on the Actor model (blogged about a long time ago) which, if your a Java developer, should hopefully lead you to the [Akka](http://akka.io/) toolkit and runtime for some home study.  Time to embrace the Actor model?

~ by mdavey on October 28, 2015.

Posted in [Languages](https://mdavey.wordpress.com/category/languages/)