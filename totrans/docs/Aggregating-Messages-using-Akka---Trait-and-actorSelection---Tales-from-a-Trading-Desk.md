<!--yml
category: 未分类
date: 2024-05-18 05:54:46
-->

# Aggregating Messages using Akka – Trait and actorSelection | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2014/01/22/aggregating-messages-using-akka-trait-and-actorselection/#0001-01-01](https://mdavey.wordpress.com/2014/01/22/aggregating-messages-using-akka-trait-and-actorselection/#0001-01-01)

## Aggregating Messages using Akka – Trait and actorSelection

Whilst on the plane back from NY recently I began to ponder about the [aggregation](http://techblog.net-a-porter.com/2013/12/ask-tell-and-per-request-actors/) pattern and [akka](http://www.akkaessentials.in/2012/03/word-count-mapreduce-with-akka.html).  Luckily, it would appear that [Jamie](http://jaxenter.com/tutorial-asynchronous-programming-with-akka-actors-46220.html) Allen, followed by a [few](https://vaughnvernon.co/?p=539) other [bloggers](http://s-akara.blogspot.co.uk/2013/08/an-aggregator-pattern-for-akka-actor.html) have a solution that is well documented – the [aggregator](http://doc.akka.io/docs/akka/snapshot/contrib/aggregator.html) [trait](https://github.com/akara/samples/blob/master/aggregator/src/main/scala/org/akara/samples/aggregator/Aggregator.scala).

So, if I use the actorSelection to fire off messages to a group of identical actors e.g. algo’s or some such thing;

```

context.actorSelection("../<Parent>/*") ! <message>

```

I need to use the expect rather than the expectOnce to process the replies

```

context.actorSelection("../<Parent>/*") ! <message>

expect {

case <response> =>

...

collectAllResponse()

}

```

In the Akka aggregator pattern [documentation](http://doc.akka.io/docs/akka/snapshot/contrib/aggregator.html), there is a results.size check to known when you have all the response messages (or timeout), since you originally knew how many you had sent.  How do I know how many messages the actorSelection sent?

~ by mdavey on January 22, 2014.

Posted in [Languages](https://mdavey.wordpress.com/category/languages/)