<!--yml

类别：未分类

日期: 2024 年 05 月 18 日 06:24:18

-->

# 谷歌 Go 在银行里？ | 来自一个交易员的故事

> 来源：[`mdavey.wordpress.com/2013/06/04/google-go-in-banks/#0001-01-01`](https://mdavey.wordpress.com/2013/06/04/google-go-in-banks/#0001-01-01)

## 谷歌 Go 在银行里？ | 来自一个交易员的故事

投资银行在软件开发堆栈内部使用哪些语言/不能使用哪些语言方面一直限制较大——Java/C#/Flex/JavaScript 可能是主要选择。最近一段时间这种情况有所改变，一些银行大举进入 Python 阵营，也有一些小规模进入到 Scala ([Scala vs Go](http://www.cs.colorado.edu/~kena/classes/5828/s12/presentation-materials/smithbrentgibsonleon.pdf)) 并且更小规模地接触到 Clojure。随着 Go [1.1](http://blog.golang.org/2013/05/go-11-is-released.html) 的发布，这一事件所带来的典型网络热情也随之兴起，现在是时候投资于这种语言了吗？

首先，如果你对谷歌 Go 不太熟悉，请尝试这些链接：

+   Go 编程[语言](http://golang.org/doc/effective_go.html#web_server)

+   Rob Pike 谈谷歌 Go：并发性，类型系统，内存[管理](http://www.infoq.com/interviews/pike-google-go) 和 GC

+   “我最喜欢的编程语言：” 谷歌的 Go 令一些[程序员](http://arstechnica.com/information-technology/2013/05/my-favorite-programming-language-googles-go-has-some-coders-raving/)大呼过瘾

+   谷歌 Go：[入门](http://www.infoq.com/articles/google-go-primer)

+   Go [项目](http://code.google.com/p/go-wiki/wiki/Projects)

对 Go 的一些明显的观察：

+   Go 的主要目的出现在服务器端

+   性能，[并发性](http://blog.golang.org/2013/01/concurrency-is-not-parallelism.html)（语言原语）以及简单性是 Go 提供的一些属性

+   编译器速度很快

每个人都有自己喜欢的 IDE，我正在使用 Intellij [golang](http://plugins.jetbrains.com/plugin?pluginId=5047) IDE 插件。在用 Go 编写任何服务器应用程序之前，你可能希望查看 Wiki Go 项目。兴趣点😉包括：

+   内存缓存和 Redis

+   MongoDB 和 Neo4j

+   ZeroMQ，Kafka 和 RabbitMQ

如果你愿意扩展你所考虑的 Go 解决方案，并且体系架构会受益，你可能想一睹😉：

今天我怀疑没有人真的在投资银行领域考虑过 Go。因此即使其他方面没有，如果你碰巧有一点空余时间，Go 是一个有意思的语言来验证一些想法

~ 由 mdavey 于 2013 年 6 月 4 日发布。

发表在[语言](https://mdavey.wordpress.com/category/languages/)中

Tags: [并发性](https://mdavey.wordpress.com/tag/concurrency/)，[Go](https://mdavey.wordpress.com/tag/go/)，[Scala](https://mdavey.wordpress.com/tag/scala/)
