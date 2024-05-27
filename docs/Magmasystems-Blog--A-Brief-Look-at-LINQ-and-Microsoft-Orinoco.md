<!--yml

分类：未分类

日期：2024-05-18 04:53:22

-->

# Magmasystems Blog: 简要查看 LINQ 和微软 Orinoco

> 来源：[`magmasystems.blogspot.com/2009/05/brief-look-at-linq-and-microsoft.html#0001-01-01`](http://magmasystems.blogspot.com/2009/05/brief-look-at-linq-and-microsoft.html#0001-01-01)

本文节选自微软关于 Orinoco 的白皮书。感谢 Orinoco 团队为我提供这份资料。

让我们假设你有多个需要监控的电力仪表。“InputStream”包含一个元组流，每个元组包含一个单独仪表的电力读数。读数碰巧以功耗的 10 倍形式出现。

我们可以捕获每个读数并投影一个新的流，该流具有归一化的功耗。我们还可以创建一个滑动的三秒窗口，其中包含电表读数，我们可以对其进行计算。

var realValueStream =

来自 InputStream

选择新的 MeterWattage((double)e.Consumption / 10);

var windowedStream =

来自 e 在 realValueStream.SlidingWindow(TimeSpan.FromSeconds(3))

选择新的 MeterWattage(e.wattage);

然后，我们可以创建一个流，该流在一个滑动的三秒周期内具有平均功耗读数。

var averagedStream =

来自 e 在 windowedStream

选择新的 OneMeterAverage(CEPAggregates.Average(e.wattage));

（我认为下一个查询可能是不正确的，因为 ID 字段没有捕获在 windowedStream 中，但无论如何我都会继续举例）。

如果你想要为每个单独的电表获取 3 秒滑动平均值，你可以执行以下两个查询：

var meterStreamGroups =

来自 e 在 windowedStream

按 e.id 分组 e

var groupedAveragedStream =

来自 eb 的 meterStreamGroups

来自 e 在 eb

选择新的 MeterAverage(eb.Key, CEPAggregates.Avg(e.wattage));

现在，我们想要计算每个仪表在 3 秒窗口内的功耗比。

var sumStream =

来自 e 在 groupedAveragedStream

选择新的 MeterSum(CEPAggregates.Sum(e.wattage));

var ratioStream =

来自 e1 在 groupedAveragedStream

连接 e2 在 sumStream true 等于 true

选择新的

MeterRatio(e1.Id, e1.Wattage, e1.Wattage / e2.TotalWattage);

最后，我们只想捕捉来自电表 #2 的功耗比。

var filteredStream =

来自 e 在 ratioStream

其中 e.id == 2

选择 e；

©2009 Marc Adler - 版权所有。

这里的所有观点都是个人的，与我的雇主无关。
