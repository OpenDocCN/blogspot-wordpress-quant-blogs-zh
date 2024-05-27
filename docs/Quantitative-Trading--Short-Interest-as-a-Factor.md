<!--yml

分类：未分类

date: 2024-05-12 18:58:56

-->

# Quantitative Trading: Short Interest as a Factor

> 来源：[`epchan.blogspot.com/2014/05/short-interest-as-factor.html#0001-01-01`](http://epchan.blogspot.com/2014/05/short-interest-as-factor.html#0001-01-01)

零点对冲网的读者无疑会对这个

[图表](http://www.zerohedge.com/sites/default/files/images/user5/imageroot/2014/02/20140221_SI.png)

&&

[文章](http://www.zerohedge.com/news/presenting-most-shorted-stocks)

:

| ![](img/ddba574b72fa31c8d87f727d17a8fd0c.png "最被做空股票相对于标普 500 的累计回报率") |
| --- |
| 2013 年最被做空的股票累计回报率 |

事实上，做空兴趣（表示做空股票数量与总流通股本的比率）长期以来一直被认为是有效的因子。对我来说，反直觉的智慧是，一个股票被做空越多，其表现越好。你可能会通过说是“做空挤压”导致价格上涨，或许是因为消息面，并且股票出借者急于卖出他们持有的股票。如果你借入了这只股票做空，你的借入股票可能会被召回，在时机最不恰当的时候被迫买入平仓。但这是一种不令人满意的解释，因为这将只导致价格的短期（向上）势头，而不是最被做空股票的持续超越表现。这种长期超越表现似乎暗示做空者不如普通交易者信息灵通，这是奇怪的。

无论解释如何，我都很好奇短线兴趣是否真的是一个好的因子，可以长期纳入全面因子模型中。

结果？并不特别令人印象深刻。结果表明，2013 年是对这个因子来说最好的一年（因此上述令人印象深刻的图表）。那一年，一个每日重新平衡的多空组合（在标普 500 指数中做多 50 只最被做空的股票和做空 50 只最不被做空的股票）回报率为 6.9%，夏普比率为 2，卡马尔比率為 2.9\。然而，如果我们把回测扩展到 2007 年，年化回报率仅为 2.8%，夏普比率为 0.5，卡马尔比率为 0.3\。这次回测使用了 CRSP 提供的无幸存者偏差数据，做空数据由 Compustat 提供。

以下是 2007-2013 年累计回报率图表：

| ![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiIJmlqWSyqTgIFkI2pzKLdW-eV2iPEtQx9y3IX6morpJ0U6OYl-SXMzdwrxdmqNnSBQtkN-g5YwYcSbz-o0AOtOb02YIDd-C4Zhsiodm8TQ2bnK6kIV8F6zxtuhZGsRrw55qABPA/s1600/Cumulative+Returns+of+Short+Interest+Factors+2007+to+2013.png) |
| --- |
| 根据做空兴趣构建的 LS 组合的累计回报率：2007-2013 |

有趣的是，尝试在标普 600 小盘股宇宙上应用这个方法，得到了负回报，可能意味着小盘股的做空者确实拥有更 superior 信息。

我保证，这将是我最近一次谈论因子！

===

**技术更新：**

我得知 Matlab 现在提供的许可证只需 149 美元，感到震惊——所谓的

【Matlab 主页](http://www.mathworks.com/products/matlab-home/)

(致谢：Ken H.) 此外，其交易工具箱现在提供与 Interactive Brokers 的 API 连接，以及其他一些经纪公司。我对 Matlab 和 R 都很熟悉，尽管我对 R 中免费的高级统计包数量之大数据印象深刻，但我仍然认为 Matlab 是我们开发自己策略最有效的平台。Matlab 开发（调试）环境要流畅和易用得多。这个差距比微软 Word 和谷歌文档还要大。

读者 Ravi B.告诉我，如果想尝试不同的季节性期货策略，可以访问 www.seasonalgo.com。

最后，一家初创公司位于

【inovancetech.com](http://inovancetech.com/)

提供机器学习算法，帮助你找到交易外汇的最佳技术指标组合。

====

**研讨会更新：**

我现在提供

毫秒级频率交易

（MFT）研讨会作为在线课程于 6 月 26 日至 27 日举行。此前，我只在伦敦现场提供，并给一些机构投资者提供。它有两个主要部分：

第一部分：介绍给交易员的技术，他们希望

避免

高频交易捕食者。

第二部分：如何使用 Matlab 回测需要毫秒级分辨率的 tick 数据策略。

使用的示例策略基于订单流。更多详情，请访问

【epchan.com/my-workshops](http://epchan.com/my-workshops)

。

此外，我将于 6 月 17 日至 20 日在香港举办均值回归和动量（但不是 MFT）研讨会。
