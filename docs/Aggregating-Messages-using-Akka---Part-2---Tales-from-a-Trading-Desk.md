<!--yml

分类: 未分类

日期: 2024-05-18 05:54:41

-->

# 使用 Akka 进行消息聚合 – 第二部分 | 一个交易台的故事

> 来源：[`mdavey.wordpress.com/2014/01/23/aggregating-messages-using-akka-part-2/#0001-01-01`](https://mdavey.wordpress.com/2014/01/23/aggregating-messages-using-akka-part-2/#0001-01-01)

## 使用 Akka 进行消息聚合 – 第二部分

在上一篇帖子的基础上，尝试了各种解决方案的变体，以终止[期望](http://doc.akka.io/api/akka/snapshot/index.html#akka.contrib.pattern.Aggregator)函数，而不是依赖于超时来实现 happy path，我最终得到了这个破解的解决方案

```

var count=0

...

context.children.foreach( f => {count=count+1})

```

有了 count，我现在可以有效地像其他博主的解决方案一样终止收集器。

```

def collectResults(force: Boolean = false) {
   if (results.size == count || force) {
      originalSender ! results.toList // Make sure it becomes immutable
      context.stop(self)
   }
}

```

~ 作者：mdavey，于 2014 年 1 月 23 日发布。

发布在 [语言](https://mdavey.wordpress.com/category/languages/) 中
