<!--yml

category: 未分类

date: 2024-05-18 05:54:46

-->

# 使用 Akka 进行消息聚合 - Trait 和 actorSelection | 交易台的故事

> 来源：[`mdavey.wordpress.com/2014/01/22/aggregating-messages-using-akka-trait-and-actorselection/#0001-01-01`](https://mdavey.wordpress.com/2014/01/22/aggregating-messages-using-akka-trait-and-actorselection/#0001-01-01)

## 使用 Akka 进行消息聚合 - Trait 和 actorSelection

最近在从纽约回来的飞机上，我开始思考[聚合](http://techblog.net-a-porter.com/2013/12/ask-tell-and-per-request-actors/)模式和[akka](http://www.akkaessentials.in/2012/03/word-count-mapreduce-with-akka.html)。幸运的是，[Jamie](http://jaxenter.com/tutorial-asynchronous-programming-with-akka-actors-46220.html) Allen，以及其他一些[博主](https://vaughnvernon.co/?p=539)已经提供了一种被充分记录的解决方案 - [aggregator](http://doc.akka.io/docs/akka/snapshot/contrib/aggregator.html) [trait](https://github.com/akara/samples/blob/master/aggregator/src/main/scala/org/akara/samples/aggregator/Aggregator.scala)。

因此，如果我使用 actorSelection 向一组相同的演员发送消息，例如算法或类似的东西；

```

context.actorSelection("../<Parent>/*") ! <message>

```

我需要使用 expect 而不是 expectOnce 来处理回复

```

context.actorSelection("../<Parent>/*") ! <message>

expect {

case <response> =>

...

collectAllResponse()

}

```

在 Akka 聚合器模式的 [文档](http://doc.akka.io/docs/akka/snapshot/contrib/aggregator.html) 中，有一个 results.size 的检查来知道何时收到所有响应消息（或超时），因为您最初知道已发送了多少消息。我如何知道 actorSelection 发送了多少消息？

~ 作者 mdavey 于 2014 年 1 月 22 日。

发布在 [Languages](https://mdavey.wordpress.com/category/languages/)
