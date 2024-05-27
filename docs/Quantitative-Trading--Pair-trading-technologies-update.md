<!--yml

类别：未分类

日期：2024-05-12 19:03:53

-->

# 量化交易：成对交易技术更新

> 来源：[`epchan.blogspot.com/2010/07/pair-trading-technologies-update.html#0001-01-01`](http://epchan.blogspot.com/2010/07/pair-trading-technologies-update.html#0001-01-01)

成对交易是在二十年前发明的，但自动化其实施直到最近才受到独立交易员的青睐。但一旦聚光灯照下，创新就会迅速猛烈地到来。以下是我认为有趣的几个近期发展：

1. 我提到了

以前](http://epchan.blogspot.com/2009/05/matlab-as-automated-execution-system.html)

称为

[quant2ib](http://exchangeapi.com/ProductOverview.htm)

。它是一个 API，允许我们从 Matlab 程序获取市场数据并向 Interactive Brokers（IB）发送订单。我已广泛用于我们的交易，并且它像 IB 的本地 API 一样可靠。他们最新的版本现在包括了构建“组合”证券的功能。这种组合证券可以是股票、ETF、期货等成对（值得注意的是，货币除外），API 允许您获取市场数据以及向组合提交订单。这是一个巨大的改进，因为您可以现在通过提交

限制

在组合上提交订单。（以前，您至少需要在成对的一侧提交市场订单，这需要您的程序持续监控市场价格并在适当的时候发送订单。否则，您必须放弃使用 API，并在 IB 的 TWS 中手动输入“通用组合”限价订单。）

2. Alphacet Discovery 还具有在成对上发送限价订单的能力，因为它

合作伙伴关系](http://alphacet.com/site/news/knight.shtml)

与 Knight Trading 合作。此外，根据我最近看到的演示，他们还现在拥有出色的成对投资组合和执行报告功能。（全文披露：我过去为他们提供咨询服务。）

3. IB 本身发布了一个“Scale Trader”算法，可以应用于组合（参见 1.上面。致谢：Mohamed。）我无法比他们的新闻稿更好地解释这个： “… ScaleTrader 算法允许客户创建条件，在这些条件下，同时创建一个股票的长期头寸，同时创建另一个的抵消性短期头寸。ScaleTrader 之所以得名，是因为投资者可以'

规模

设置

订单

随着市场下跌买入。同样，卖出

订单

可以在市场上升时“扩大”进入。ScaleTrader 算法可以编程购买价差，随后在价差达到用户设定的预定水平时通过卖出价差获利。"换句话说，它允许我们自动实施“

无参数交易](http://epchan.blogspot.com/2008/08/more-on-parameterless-trading-model.html)

“或“

[平均入市](http://epchan.blogspot.com/2010/01/does-averaging-in-work.html)

我之前在博客上提到的*无需我们编程*的策略。

说到配对交易，我将首次教授我的纽约*工作坊*。

[工作坊](http://www.technicalanalyst.co.uk/training/pairs-trading.htm)的链接需要保留原文网址。

在十月。](My editor inevitably picks touristy locations for these workshops. My London workshop takes place across the street from the Tower of London, my New York workshop is across from the new World Trade Center, and my Hong Kong workshop is in the "Golden Mile" shopping district of Tsim Sha Tsui.)
