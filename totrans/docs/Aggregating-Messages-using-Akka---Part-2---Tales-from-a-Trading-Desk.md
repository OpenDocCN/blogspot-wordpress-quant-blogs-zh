<!--yml
category: 未分类
date: 2024-05-18 05:54:41
-->

# Aggregating Messages using Akka – Part 2 | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2014/01/23/aggregating-messages-using-akka-part-2/#0001-01-01](https://mdavey.wordpress.com/2014/01/23/aggregating-messages-using-akka-part-2/#0001-01-01)

## Aggregating Messages using Akka – Part 2

Following on from the last posting, and trying various variants of a solution to terminate the [expect](http://doc.akka.io/api/akka/snapshot/index.html#akka.contrib.pattern.Aggregator) function rather than reply on the timeout for the happy path, I ended up with this hacked solution

```

var count=0

...

context.children.foreach( f => {count=count+1})

```

With count, I can now effectively terminate the collector as per the other bloggers solutions

```

def collectResults(force: Boolean = false) {
   if (results.size == count || force) {
      originalSender ! results.toList // Make sure it becomes immutable
      context.stop(self)
   }
}

```

~ by mdavey on January 23, 2014.

Posted in [Languages](https://mdavey.wordpress.com/category/languages/)