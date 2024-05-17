<!--yml
category: 未分类
date: 2024-05-18 06:37:01
-->

# Financial Messaging: ZeroMQ Random Reading | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2012/08/01/financial-messaging-zeromq-random-reading/#0001-01-01](https://mdavey.wordpress.com/2012/08/01/financial-messaging-zeromq-random-reading/#0001-01-01)

Bit of a spaghetti posting, but possibly relevant at a future date 😉

Although old, [Design and Evaluation of Benchmarks for Financial Applications using Advanced Message Queuing Protocol (AMQP) over InﬁniBand](ftp://ftp.cse.ohio-state.edu/pub/tech-report/2008/TR51.pdf) is worth a read in the context of Martin’s [comments](https://groups.google.com/forum/?fromgroups#!topic/lmax-disruptor/CFXHbAYqmIs) around the disruptor, Ultra Messaging and ZeroMQ (ØMQ)

> 0MQ did not exist when we evaluated message providers.  This was about
> 3 years ago.  It does look interesting for some usecases.
> 
> When going for ultra low-latency you need to pick a transport that
> uses IP multicast or InfiniBand.  TCP has significant overhead, and
> buffering, which does not lend itself to low-latency.  It is also
> important to pick a transport that does not use daemons/brokers.
> These “men in the middle” add latency and can be single points of
> failure.  State of the art is single digit microseconds for a hop
> between two nodes.  Have you measured 0MQ?

Which leads to Mr Fowler’s overview of the [LMAX](http://martinfowler.com/articles/lmax.html) architecture, and specifically the details on replication and master/slave:

> Earlier on I mentioned that LMAX runs multiple copies of its system in a cluster to support rapid failover. The replicator keeps these nodes in sync. All communication in LMAX uses IP multicasting, so clients don’t need to know which IP address is the master node. Only the master node listens directly to input events and runs a replicator. The replicator broadcasts the input events to the slave nodes. Should the master node go down, it’s lack of heartbeat will be noticed, another node becomes master, starts processing input events, and starts its replicator. Each node has its own input disruptor and thus has its own journal and does its own unmarshaling.
> 
> Even with IP multicasting replication is still needed because IP messages can arrive in a different order on different nodes. The master node provides a deterministic sequence for the rest of the processing.

Which leads to a few relevant articles over on the ZeroMQ site (assuming you happened to want to look at ZeroMQ in this context, and didn’t want to pay for Ultra Messaging):

~ by mdavey on August 1, 2012.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)
Tags: [Disruptor](https://mdavey.wordpress.com/tag/disruptor/), [Messaging](https://mdavey.wordpress.com/tag/messaging/)