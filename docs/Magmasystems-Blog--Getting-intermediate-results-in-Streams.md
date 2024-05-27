<!--yml

category: 未分类

日期：2024 年 5 月 18 日 05:05:47

-->

# Magmasystems Blog: 获取流中的中间结果

> 来源：[`magmasystems.blogspot.com/2007/12/getting-intermediate-results-in-streams.html#0001-01-01`](http://magmasystems.blogspot.com/2007/12/getting-intermediate-results-in-streams.html#0001-01-01)

比方说我们希望对我们交易的股票数量进行累加总，每天下午 4 点时，我们希望倾倒出总数。在 Coral8 中，我们可以这样做：

创建本地流 Totals (TotalShares INTEGER);INSERT INTO TotalsSELECT SUM(shares) FROM TradeInputStream KEEP EVERY 1 DAY OFFSET BY 16 HOURS OUTPUT EVERY 1 DAY OFFSET BY 16 HOURS;

这看起来很简单。Totals 流保留了累加总数，直到下午 4 点。每天下午 4 点，它会将总股票数输出到任何其他订阅 Totals 的流中，然后重置自身以开始累积新的总数。

这是

CEP

引擎擅长的技术，无论是 Coral8，

Aleri

，或者

Esper

。

现在，让我们稍微完善一下。

比方说我们给交易员一个 .NET 的 GUI 应用程序，在这个 GUI 上有一个“状态”按钮。交易员可以随时按下此按钮，以了解当天到目前为止已经交易了多少股票。因此，在 2 点，交易员在 GUI 上按下一个按钮，我们需要向他返回当天迄今为止看到的订单数、看到的股票数、所有订单的名义价值等。

所以，有两个问题：

1）我们如何按需“倾倒”这些累加器？换句话说，是否有办法告诉这些

CEP

引擎来给我聚合流的内容直到此时？

2）我们如何“调用到”我们的

CEP

引擎来检索这些值？这些

CEP

引擎支持一个

应用程序接口（API）

我可以在 GUI 内部使用，说“给我模块中某个变量的当前值”？这样的东西

IntegerFieldValue field = Coral8Service.GetObject("ccl://localhost:6789/Default/SectorFlowAnalyzer", "sum(Shares)") as IntegerFieldValue; int shares = field.Value;

在标准的 C# 应用程序中，这就像给一个变量放一个 Getter，并且调用 Getter 一样简单。如果我要使用 Web 服务，那么我可以调用一个 Web 服务，然后询问一些变量的值或某种对象的值。

***但是，从 C# 应用程序中，我怎么才能得到一个正在聚合总数的流的当前值？***

累积一个

CEP

引擎是进入过程化世界，只需定义一个变量。在 Coral8 中，就像这样：

创建变量 TotalShares INTEGER = 0;ON TradeInputStreamSET TotalShares = TotalShares + TradeInputStream.shares;

然后，我们需要每天下午 4 点触发一个“脉冲”，当这个脉冲触发时，我们可以发送

TotalShares

到另一个流。

我确信每个复杂事件处理(CEP)引擎都有访问中间结果的模式，但在 CEP 供应商的 SQL 变体中，那些在过程式语言中显而易见的东西可能并不那么容易。

©2007 Marc Adler - 版权所有
