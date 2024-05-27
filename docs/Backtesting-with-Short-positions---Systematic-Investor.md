<!--yml

分类：未分类

日期：2024-05-18 14:45:09

-->

# 使用空头策略进行回测 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2011/12/02/backtesting-with-short-positions/#0001-01-01`](https://systematicinvestor.wordpress.com/2011/12/02/backtesting-with-short-positions/#0001-01-01)

我想说明使用 [Woodshedder](http://ibankcoin.com/woodshedderblog/author/woodshedder/) 在 [Simple, Long-Term Indicator Near to Giving Short Signal](http://ibankcoin.com/woodshedderblog/2011/08/28/simple-long-term-indicator-near-to-giving-short-signal/) 文章中介绍的一种有趣策略进行空头回测。这个策略也在 MarketSci 的 [Woodshedder’s Long-Term Indicator](http://marketsci.wordpress.com/2011/10/04/woodshedders-long-term-indicator/) 文章中进行了详细分析。

该策略使用了 5 天变化率（ROC5）和 252 天变化率（ROC252）：

+   如果昨天的 ROC252 上穿 ROC5，并且今天的 ROC252 仍然高于 ROC5，则在收盘时买入（或平空仓）。

+   如果昨天的 ROC5 上穿 ROC252，并且今天的 ROC5 仍然高于 ROC252，则在收盘时卖出（或开空仓）。

以下是使用 [Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/) 中的回测库实现此策略的示例代码：

```

# Load Systematic Investor Toolbox (SIT)
setInternet2(TRUE)
con = gzcon(url('https://github.com/systematicinvestor/SIT/raw/master/sit.gz', 'rb'))
	source(con)
close(con)

	#*****************************************************************
	# Load historical data
	#******************************************************************
	load.packages('quantmod')
	tickers = spl('SPY')

	data 	getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)
	bt.prep(data, align='keep.all', dates='1970::2011')

	#*****************************************************************
	# Code Strategies
	#******************************************************************
	prices = data$prices

	# Buy & Hold
	data$weight[] = 1
	buy.hold = bt.run(data)

	# ROC Strategy
	roc5 = prices / mlag(prices,5)
	roc252 = prices / mlag(prices,252)
		roc5.1 = mlag(roc5,1)
		roc5.2 = mlag(roc5,2)
		roc252.1 = mlag(roc252,1)
		roc252.2 = mlag(roc252,2)

	data$weight[] = NA
		data$weight$SPY[] = iif(roc252.2 < roc5.2 & roc252.1 > roc5.1 & roc252 > roc5, 1, data$weight$SPY)
		data$weight$SPY[] = iif(roc252.2 > roc5.2 & roc252.1 < roc5.1 & roc252 < roc5, -1, data$weight$SPY)
	roc.cross = bt.run(data, trade.summary=T)

	#*****************************************************************
	# Create Report
	#******************************************************************
	plotbt.custom.report(roc.cross, buy.hold, trade.summary=T)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot1-small10.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot2-small9.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot3-small7.png)

对比 ROC 策略的资产曲线和 Woodshedder 显示的资产曲线，可以快速发现有显著差异。ROC 策略的资产曲线在 2008-2009 年达到峰值，而 Woodshedder 显示的资产曲线在 2011 年达到峰值。我在 Amibroker 中重新创建了这个策略，并得到了与 Woodshedder 报告的结果相似的结果。那么问题出在哪里呢？

问题出在创建回测的方式上，我使用的是权重，而不是股票来创建回测。让我们比较当每个时期价格上涨 10％时，使用权重或股票的**多头策略**的回测表现：

| P0 | P1 | P2 |
| --- | --- | --- |
| 100 | 110 | 121 |
|  | R1 | R2 |
|  | 10% | 10% |

使用一份股票的总回报，[(一份股票) * P2] / 100 – 1 = 21％，使用权重的总回报，(1+R1)(1+R2) – 1 = 21％，完全相同。

考虑每个时期价格下跌 10％时使用**空头策略**的表现：

| P0 | P1 | P2 |
| --- | --- | --- |
| 100 | 90 | 81 |
|  | R1 | R2 |
|  | -10% | -10% |

使用一份股票的总回报，[200 – (一份股票) * P2] / 100 – 1 = 19％，使用权重的总回报，(1+R1)(1+R2) – 1 = 21％，不同。

差异出现在期间 1，价格下跌了 10%，因此我们有额外的$10 要投资。因此，如果收益重新投资，期间 0 的投资组合价值为$100，在期间 1 为$110 = 1.1 * $100，在期间 2 为$121 = 1.1 * $110，总回报为$121 / $100 – 1 = 21%。

总之，如果使用空头回测，我们不能使用权重*收益来计算投资组合回报，因为它假设所有的盯市盈利立即重新投资，而是应该使用股票来创建回测。

这里是实现股票回测（在`bt.run`函数中 type='share'）的代码：

```

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 	
	# If Backtesting with Short positions, always use type = 'share' backtest to get realistic results.
	data$weight[] = NA
		data$weight$SPY[] = iif(roc252.2 < roc5.2 & roc252.1 > roc5.1 & roc252 > roc5, 1, data$weight$SPY)
		data$weight$SPY[] = iif(roc252.2 > roc5.2 & roc252.1 < roc5.1 & roc252 < roc5, -1, data$weight$SPY)	

		capital = 100000
		data$weight[] = (capital / prices) * bt.exrem(data$weight)
	roc.cross.share = bt.run(data, type='share', trade.summary=T)							

	#*****************************************************************
	# Create Report
	#******************************************************************
	plotbt.custom.report(roc.cross.share, roc.cross, buy.hold, trade.summary=T)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot4-small3.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot5-small2.png)

最后，使用回测中的 type='share'的 ROC 策略的股票曲线与 Woodshedder 报告的曲线非常相似。

要查看此示例的完整源代码，请查看[github 上的 bt.test.r 中的 bt.roc.cross.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
