<!--yml

类别：未分类

日期：2024-05-18 14:43:31

-->

# 时间序列匹配策略回测 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/01/17/time-series-matching-strategy-backtest/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/01/17/time-series-matching-strategy-backtest/#0001-01-01)

这篇文章是为了回应在[时间序列匹配](https://systematicinvestor.wordpress.com/2012/01/13/time-series-matching/)文章中提出的评论。我将展示一个非常简单的回测时间序列匹配策略的例子，使用距离加权预测。我必须警告你，这个策略的表现不如买入持有策略。

我使用了来自[时间序列匹配](https://systematicinvestor.wordpress.com/2012/01/13/time-series-matching/)文章的代码，并将其重新组织成 3 个函数：

bt.matching.find – 寻找与给定查询（模式）相似的历史匹配。

bt.matching.overlay – 创建一个矩阵，将所有匹配项叠加在一起。

bt.matching.overlay.table – 创建并绘制匹配摘要表。

我将使用[^GSPC](http://finance.yahoo.com/q?s=%5Egspc)的历史价格来扩展[SPY](http://finance.yahoo.com/q?s=spy)的时间序列。我将创建一个月的回测，在月底交易，始于 1994 年 1 月。每个月，我将回顾过去 10 年历史中的最后 90 天，寻找最佳的历史匹配。

我将计算下一个月的历史加权平均预测，如果预测为正则做多，否则持有现金。这是一个非常简单的回测，该策略的表现不如买入持有策略。

以下代码从雅虎财经加载历史价格，并使用[系统投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)设置时间序列匹配策略回测：

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)
###############################################################################
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')	
	tickers = spl('SPY,^GSPC')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1950-01-01', env = data, auto.assign = T)
	bt.prep(data, align='keep.all')

	# combine SPY and ^GSPC
	scale = as.double( data$prices$SPY['1993:01:29'] / data$prices$GSPC['1993:01:29'] )
	hist = c(scale * data$prices$GSPC['::1993:01:28'], data$prices$SPY['1993:01:29::'])

	#*****************************************************************
	# Backtest setup:
	# Starting January 1994, each month search for the 10 best matches 
	# similar to the last 90 days in the last 10 years of history data
	#
	# Invest next month if distance weighted prediction is positive
	# otherwise stay in cash
	#****************************************************************** 
	month.ends = endpoints(hist, 'months')
		month.ends = month.ends[month.ends > 0]		

	start.index = which(date.year(index(hist[month.ends])) == 1994)[1]
	weight = hist * NA

	for( i in start.index : len(month.ends) ) {
		obj = bt.matching.find(hist[1:month.ends[i],], normalize.fn = normalize.first)
		matches = bt.matching.overlay(obj)

		# compute prediction for next month
		n.match = len(obj$min.index)
		n.query = len(obj$query)				
		month.ahead.forecast = matches[,(2*n.query+22)]/ matches[,2*n.query] - 1

		# Distance weighted average
		temp = round(100*(obj$dist / obj$dist[1] - 1))		
			n.weight = max(temp) + 1
			weights = (n.weight - temp) / ( n.weight * (n.weight+1) / 2)
		weights = weights / sum(weights)
			# barplot(weights)
		avg.direction = weighted.mean(month.ahead.forecast[1:n.match], w=weights)

		# Logic
		weight[month.ends[i]] = 0
		if( avg.direction > 0 ) weight[month.ends[i]] = 1
	}

```

接下来，让我们比较时间序列匹配策略与买入持有策略：

```

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 
	tickers = 'SPY'

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1950-01-01', env = data, auto.assign = T)
	bt.prep(data, align='keep.all')

	prices = data$prices  

	# Buy & Hold	
	data$weight[] = 1
	buy.hold = bt.run(data)	

	# Strategy
	data$weight[] = NA
		data$weight[] = weight['1993:01:29::']
		capital = 100000
		data$weight[] = (capital / prices) * bt.exrem(data$weight)
	test = bt.run(data, type='share', capital=capital, trade.summary=T)

	#*****************************************************************
	# Create Report
	#****************************************************************** 
	plotbt.custom.report.part1(test, buy.hold, trade.summary=T)

```

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/01/plot1-small2.png)

你会如何改变策略或回测使其盈利？请分享你的想法。我期待着探索它们。

要查看这个例子完整的源代码，请查看 github 上的 [bt.matching.backtest.test() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
