<!--yml

分类：未分类

日期：2024-05-12 19:30:40

-->

# RethinkDB 入门 | 编码市场

> 来源：[`etrading.wordpress.com/2016/04/21/starting-out-with-rethinkdb/#0001-01-01`](https://etrading.wordpress.com/2016/04/21/starting-out-with-rethinkdb/#0001-01-01)

## RethinkDB 入门

### 2016 年 4 月 21 日

我一直想为基于云的 [SpreadServe](http://spreadserve.com/) 服务使用 [RethinkDB](https://rethinkdb.com/)，所以当我听说 Windows 版本已经进入 beta 阶段时，就没有理由再延迟了。现在，NoSQL 数据库非常流行，有 [Mongo](https://www.amon.cx/blog/rethinkdb-reviewed-by-a-mongo-fan/)、[Cassandra、Couch 和 Redis](http://kkovacs.eu/cassandra-vs-mongodb-vs-couchdb-vs-redis) 等供选择。对我来说，RethinkDB 有几个突出的原因。首先，它的 [changefeeds](https://rethinkdb.com/docs/changefeeds/python/)。所有分布式系统都必须解决将进程缓存与数据库同步的挑战。我在过去几年里在一些大型银行见过两种高质量的手动解决方案。一个基于 SQL Server 触发器，导致以 XML 格式广播更新或插入的行。而在 [JP Morgan's Athena](http://techcareers.jpmorgan.com/cm/BlobServer/athena_jpmc.pdf) 项目中，我看到使用 [Twisted](https://github.com/twisted/twisted) 对象序列化来更新套接字订阅者的最近更改的对象。两种方法都很好地扩展了。RethinkDB 的特殊之处在于，它通过 changefeeds 为您解决了这个问题。RethinkDB 对我吸引的第二个特性是，Python API 是一流的公民，而不是事后想到的。Python API 的事件处理和协程实现风格与我也在 SpreadServe 中使用的 [Tornado](http://www.tornadoweb.org/en/stable/) 很好地集成在一起。第三，我喜欢的是 RethinkDB 的核心实现是用 C++ 编写的，并且是开源的。像 RethinkDB 一样，JP 的 Athena，SpreadServe 在内部也是 C++，具有 Python API。

我已经在几天内使用 [RethinkDB 2.3.0 beta build for Windows](https://rethinkdb.com/docs/install/windows/)。 Rethink 的几个方面让我感到高兴，但也遇到了一些问题。我也意识到，转向基于协程的编码是一件大事。所以让我在这里记录一下。首先是让我感到高兴的事情...

+   安装过程非常简单

+   不错的文档

+   良好的管理 UI：数据浏览器非常好。

这是我遇到的问题...

+   在 Python 中编码时，不要忘记在 r.table( ).get( ) 或 r.table( ).insert( ) 后面加上 .run( )

+   方法名称在不同的 API 中不一致。例如，在 JS 中是 getAll( )，而在 Python 中是 get_all( )。即使你像我一样在 Python 中编码，你仍然会发现自己在管理界面的数据浏览器中使用 JS，所以这是一个烦恼。

+   你需要 tornado 4 或更高版本，因为 RethinkDB 的 Tornado 集成导入了 tornado.tcpclient，这在 3.x 中是没有的。我花了一段时间才追踪到这个问题，因为与我连接的 RethinkDB 的服务器进程默默退出，日志或控制台没有任何导入错误的信息。然而，Python 文档确实提到，im.load_module()，像在 r.set_loop_type()中使用，可能会抛出 ImportError。一旦我在 r.set_loop_type()周围加上 try/except 语句，我就捕获了异常，并意识到我需要从 Tornado 3.2 升级到 4.2.1。

一旦我解决了这些陷阱，我意识到我需要升级我的编程风格来拥抱协程。它们自 Python 2.7 起就已经存在，Tornado 也已经采用了它们。RethinkDB 示例中到处都是协程。过去的十年里，我一直以单线程或低线程异步回调风格进行编程，意识到多线程阻塞工作线程方法效率低下，且容易导致死锁和竞态条件。但我的所有代码都非常依赖于回调，协程与那是一个很大的转变。过去几天我面临的一个大挑战就是弄清楚如何结合这两种风格。我自己的 C++和 Python 框架使用单线程异步风格。而且我还有一堆与这种风格相同的基于 Tornado 的代码。现在我需要将这个与以协程风格编写的 RethinkDB 代码结合起来。我找到了一篇关于如何将回调风格的 Tornado 代码重构为使用协程的精彩博客文章：[`emptysqua.re/blog/refactoring-tornado-coroutines/`](https://emptysqua.re/blog/refactoring-tornado-coroutines/)

这对我帮助极大。我所犯的一个错误是认为 Rethink/Tornado 协程可以直接像生成器那样调用。它们不能，你必须使用 loop.add_callback()来调度它们。我会在更深入探索 RethinkDB 和协程后带来更多内容，我计划分享更多像这样的[Tornado Web 服务器的最小化、完整 Gist](https://gist.github.com/osullivj/e0faf2348528285a388b74e398307bae)与 RethinkDB changefeed 的代码样本。
