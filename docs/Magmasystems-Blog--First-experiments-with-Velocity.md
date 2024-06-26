<!--yml

分类：未分类

日期：2024-05-18 05:00:35

→

# Magmasystems 博客：使用 Velocity 的第一次实验

> 来源：[`magmasystems.blogspot.com/2008/07/first-experiments-with-velocity.html#0001-01-01`](http://magmasystems.blogspot.com/2008/07/first-experiments-with-velocity.html#0001-01-01)

我对

**Microsoft Velocity**

这个周末，我组装了一个小型的订单缓存应用。这个应用可以读取

**FIX**

从

**Tibco EMS**

总线，把消息转换成 C#对象，并把对象存入 Velocity 缓存中。

订单缓存的主键是

**ClOrdId**

，并且这个值对于每个交易日都应该是唯一的。每次我们看到一个 FIX 消息，我们就检查缓存中是否有一个相同的 ClOrdId 的对象。如果有，订单对象就会被更新，并把对象重新存入缓存。保持订单和执行状态，数量被更新，取消和取消/替换被核算。

坦白说，这是一个极其简单的应用，但我这么做只是为了熟悉 Velocity 的第一个 CTP 版本。一个缓存持有所有订单对象。我没有尝试按符号在不同缓存中对订单进行 alpha 分区，也没有尝试多个区域。仅仅是简单的获取、放置和添加。我稍微用了 Reflector 来窥视 Velocity 的代码，并且我能看到 Velocity 表面之下还有许多尚未暴露的东西。

我们可以在复杂事件处理系统中使用对象缓存的地方在哪里？

首先，我们可以用它来支持 CEP 系统的弹性。比如说我们的 CEP 引擎在一天的中间崩溃了。我们希望能够检索到我们订单和执行的当前状态，但我们不想回到某种 FIX 仓库，再回放每一个 FIX 消息来重新创建 CEP 引擎的状态。我们可以使用对象缓存来帮助恢复状态。

现在，大多数 CEP 引擎都有保存状态的功能。例如，使用 Coral8，你可以选择每隔 n 秒或分钟将所有窗口保存到数据库中。但是，处理实时数据快速流的 CEP 引擎的状态持久化存在一定的紧张关系。如果你频繁地持久化，可能会减慢 CEP 引擎的速度。如果你不频繁地持久化，那么如果 CEP 引擎失败，你可能会丢失大量的状态。

大多数 CEP 引擎将使用外部数据库，如 SleepyCat、BerkeleyDB 和 SQL Server 来存储状态。但是，根据您保存数据的规模和形状，恢复可能会很慢。那么，为什么不保存到对象缓存中呢？对对象缓存的读写速度会非常快，如果对象缓存支持异步将数据存储到后端数据库（或微软的 SSDS），那么你就可以兼得鱼和熊掌。

在各种 CEP 引擎中，我还没有看到任何内置适配器支持对象缓存，如 Gemfire、Tangasol、GigaSpaces 和 Velocity。编写一个并不困难，但需要在本地 C#对象和类似 Coral8 元组之间进行序列化。

**愿望#1：事件处理引擎供应商探索对象缓存作为持久化的方法。**

对象缓存的一种其他用途是协助查询界面。像 Coral8 这样的 CEP 引擎支持对窗口的即兴查询。如果 CEP 引擎正在聚合像订单和执行数据这样的数据，并且这些数据是在一个可以公开查询的窗口内，任何应用程序都应该能够查询 CEP 引擎，例如“10:15 至 10:30 之间有哪些拥有开放订单的前十大股票”。

我们不希望外部应用程序直接连接到 CEP 引擎。涉及合规性和安全问题，我们也不希望任何应用程序绑定到特定版本的流式 SQL。（注：Coral8 中嵌入了 SQLite，这就是你用来查询公共窗口的东西。）因此，我们想要提供一个“查询界面”。所有应用程序都必须连接到查询界面，以便对 CEP 引擎进行即兴查询。

在 CEP 引擎处理大量流数据的同时执行即兴查询是有成本的。而且，除非你正确地索引公共窗口，否则即兴查询可能会非常慢。

那么，为什么不能查询对象缓存呢？如果我们将在 Velocity 中存储聚合的订单和执行数据，为什么我们不能查询 Velocity 以找到 10:15 至 10:30 之间有开放订单的前十大股票呢？换句话说，查询对象缓存应该与查询 SQL Server 数据库几乎一样。我不在乎查询语言是 SQL 92、流式 SQL、LINQ 还是 SSDS 有的那种 LINQ 式的玩意……只要不是 Q 就行了。

**愿望#2：微软将与对象缓存和 CEP 引擎供应商共同制定一种通用方法，用于查询数据库、缓存和 CEP 引擎。**

©2008 Marc Adler - 版权所有。

所有意见均属个人，与我的雇主无关。
