请注意，以上只是部分翻译内容，如果需要更多翻译或者有其他需求，请告知。

类别：未分类

日期：2024-05-18 05:06:29

→

# Magmasystems Blog: 关于第一个 CEP 用例的更多内容

> 来源：[`magmasystems.blogspot.com/2007/11/more-on-first-cep-use-case.html#0001-01-01`](http://magmasystems.blogspot.com/2007/11/more-on-first-cep-use-case.html#0001-01-01)

昨天，我与 Coral8 的 Henry 和 Bob 进行了一场两个小时的会议，其中完成了大多数用例。

Henry 是我们的指定预销售工程师。他的工作是要确保潜在客户在决定购买产品之前对产品感到满意。Bob 是 Coral8 的首席架构师，他的工作（正如他描述的）是要确保产品尽可能容易使用。

在亨利和鲍勃之间，提出了两个解决方案。我将在本文中介绍第一个解决方案。第二个解决方案涉及输入适配器自定义消息时间戳，这个话题值得单独一篇博客文章。

主要问题是要分析每个部门在一分钟时间片内的订单流程，并确定是否有任何部门显示出异常活动。我所面临的问题是“时间”的概念由 FIX 消息中的 TransactTime 字段决定，而不是由墙上的“时钟”决定。所以，如果出于某种原因，我连续收到两个 FIX 消息，其中一个的 TransactTime 字段是 14:24:57，另一个的 TransactTime 字段是 14:25:01，那么收到第二个 FIX 消息应该会导致一个新的时间片，而不管墙上的时钟显示什么。

亨利提出的解决方案是在流中使用脉冲。尽管在编程中 raising 事件的概念非常普遍，但在 SQL 存储过程中并不是真正要做的事情。事情在于，Coral8 的 CCL（以及许多 CEP 供应商的 SQL 样式的方言）编程是一种过程编程和 SQL 编程的组合，找到解决您问题的正确“模式”是关键。这是许多 CEP 供应商可以改进的地方；他们可以发布模式列表，他们可以制定常见问题解答等。我将这一点告诉了 Coral8 的 Bob，所以期待 Coral8 方面在这方面有一些进展。

以下是 Coral8 的 CCL 中脉冲流的显示方式：

----------------------------------------------------------------------------------

LastTimeSlice 保持订单流的最大时间片（0 到 389）。

当我们看到一个 TransactTime 大于当前最大时间片的订单时，

然后我们设置新的最大时间片。我们还将此用作一个信号（脉冲）

将文本输入到以下流之一中。

----------------------------------------------------------------------------------

创建变量整数 LastTimeslice = -1；

创建本地流 stream_Pulse；

插入到 stream_Pulse

选择

按时间时间桶(FlattenNewOrder.TransactTime) AS 时间戳

从

扁平化新订单

WHERE

按时间时间桶(FlattenNewOrder.TransactTime) > LastTimeSlice；

-- 当我们向 stream_Pulse 流中插入一个新的时间片时，我们也

-- 设置新的最大时间片。

在流 stream_Pulse 上

设置 LastTimeSlice = stream_Pulse.epoch;

我们有一个全局变量，用于记录通过我们系统的时间片中最大的时间片。由于交易日是 6.5 小时，所以我们想要考虑 390 个分钟大小的 时间片。

在 INSERT 语句中，如果来自 FIX 消息的时间片大于当前的最大时间片，那么我们在脉冲流中插入一条新记录。

ON 语句像一个触发器。当一条新记录插入到一个流中时，你可以有一个或多个 ON 语句对记录插入流的事件做出反应。在这里，我们设置新的最大时间片。

我们需要维护一个包含当前时间片所有订单的窗口。订单信息包括股票代码，股票所属的行业，订单中的股票数量和当前的时间片。在 Coral8 中，一个窗口提供了记录的保留。您可以在窗口上指定一个保留策略，无论是基于时间的时间保留策略（在窗口中保留记录 5 分钟）还是基于行的保留策略（只保留最后 100 行）。这里缺失的是基于布尔表达式或基于某些列值变化的保留策略。Streambase 具有这个功能，Coral8 知道这个特性应该在未来实现。

----------------------------------------------------------------------------------

-- TickerAndSector 窗口包含了当前时间片的所有 FIX 订单。

-- 窗口的每一行都包含 FIX 订单和行业信息。

-- 当我们看到一个新的时间片时，TickerAndSector 窗口被清空

-- 使用 DELETE 语句。

----------------------------------------------------------------------------------

创建 TickerAndSector 窗口

表结构如下：（股票代码 STRING, 行业名称 STRING, 行业 ID INTEGER, 股票数量 INTEGER, 交易时间桶 INTEGER）

保留所有记录；

向 TickerAndSector 表中插入数据

选择

FlattenNewOrder.Ticker,

TickerToSectorMap.SectorName,

TickerToSectorMap.SectorId,

插入 FlattenNewOrder.Qty 的整数形式，

TimeToTimeBucket(FlattenNewOrder.TransactTime)

从

FlattenNewOrder,

TickerToSectorMap

其中

TickerToSectorMap.Ticker = FlattenNewOrder.Ticker

AND TimeToTimeBucket(FlattenNewOrder.TransactTime) >= LastTimeSlice;

如今我们已经有了一个当前时间片内发生的订单列表，我们需要知道何时会出现新的时间片。在此时，我们需要分析当前时间片内的订单，找出哪些行业显示出异常活动，并清空 TickerAndSector 窗口，以便新的订单可以积累到新的时间片。

----------------------------------------------------------------------------------

-- 每个行业每分钟订单窗口包含聚合总数

-- 针对上一个时间片每个行业。聚合总数包括

-- 每个部门订单数量以及每个部门股票总数。

--

-- 这段代码的有趣之处在于 TickerAndSector 窗口

-- 以及 stream_Pulse。当看到新的

-- 时间片时触发。

--

-- 当我们在 OrdersPerSectorPerMinute 窗口中插入行时，我们将触发

-- TickerAndSector 窗口的旧信息删除。

----------------------------------------------------------------------------------

CREATE WINDOW OrdersPerSectorPerMinute

SCHEMA (SectorName STRING, SectorId INTEGER, OrderCount INTEGER, TotalShares INTEGER, Timeslice INTEGER)

KEEP 2 MINUTES;

INSERT INTO OrdersPerSectorPerMinute

SELECT

tas.SectorName, tas.SectorId, COUNT(*), SUM(tas.Shares), stream_Pulse.epoch

FROM

TickerAndSector tas, stream_Pulse

GROUP BY

tas.SectorId;

ON OrdersPerSectorPerMinute

DELETE FROM TickerAndSector

WHERE TransactTimeBucket < LastTimeSlice;

正如您从上面的代码中看到的，当一个新的时间片出现时，我们对 TickerAndSector 窗口中的订单数量和股票总数进行了汇总。这里有趣的是，也是我可能自己没有想出来的事情，那就是我们需要与之前提到的脉冲流进行连接。这里的脉冲流用于“启动”当前时间片的记录计算和倾倒。

最后，由于我们已经对当前时间片内的每个部门的信息进行了汇总，所以我们想看看是否有任何部门超过了最大“正常”订单数量。

----------------------------------------------------------------------------------

-- 这个输出流将在部门超过

-- 该时间片最大订单数。

----------------------------------------------------------------------------------

INSERT INTO AlertStream

SELECT

R.SectorId, R.SectorName, R.OrderCount, R.TotalShares

FROM

OrdersPerSectorPerMinute AS R, NormalOrdersPerSectorPerTimeslice AS H

WHERE

R.SectorId = H.SectorId AND R.Timeslice = H.Timeslice AND R.OrderCount > H.MaxOrders;

然后，就这样！如果我们给 AlertStream 添加一个 JMS 输出适配器，我们可以生成一个新的、派生的事件，将该事件放回 EMS 总线（或者我们可以将其发送到另一个 Coral8 流），并警报某种监控应用程序。

感谢 Coral8 的同事们帮助我艰难地走过了学习过程。

©2007 Marc Adler - 版权所有
