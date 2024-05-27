<!--yml

类别：未分类

日期：2024 年 5 月 18 日 14:41:04

-->

# 通过波动性仓位调整来改善风险调整后的绩效 | 系统性投资者

> 来源：[`systematicinvestor.wordpress.com/2012/05/01/volatility-position-sizing-to-improve-risk-adjusted-performance/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/05/01/volatility-position-sizing-to-improve-risk-adjusted-performance/#0001-01-01)

[主页](https://systematicinvestor.wordpress.com/ "转到主页")

[回测](https://systematicinvestor.wordpress.com/category/backtesting/)

,

[组合构建](https://systematicinvestor.wordpress.com/category/portfolio-construction/)

,

[R](https://systematicinvestor.wordpress.com/category/r/)

,

[策略](https://systematicinvestor.wordpress.com/category/strategy/)

,

[交易策略](https://systematicinvestor.wordpress.com/category/trading-strategies/)

> 通过波动性仓位调整来改善风险调整后的绩效

## 通过波动性仓位调整来改善风险调整后的绩效

今天我想展示如何使用波动性仓位调整来改善策略的风险调整后的绩效。我将使用[真实波动幅度（ATR）](http://stockcharts.com/school/doku.php?id=chart_school:technical_indicators:average_true_range_atr)作为波动性的衡量标准，并将在低波动期间增加分配，在高波动期间减少分配。以下是两个详细解释这些策略的良好参考资料：

首先，让我们加载 SPY 的价格，并使用[系统性投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)计算买入并持有的绩效：

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)
# https://systematicinvestor.wordpress.com/systematic-investor-toolbox/
###############################################################################
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')	
	tickers = spl('SPY')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)			
	bt.prep(data, align='keep.all', dates='1970::')	

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 
	prices = data$prices   
	nperiods = nrow(prices)

	models = list()

	#*****************************************************************
	# Buy & Hold
	#****************************************************************** 
	data$weight[] = 0
		data$weight[] = 1
	models$buy.hold = bt.run.share(data, clean.signal=T)

```

接下来，让我们修改买入并持有策略，根据[真实波动幅度（ATR）](http://stockcharts.com/school/doku.php?id=chart_school:technical_indicators:average_true_range_atr)来变化其分配。

```

	#*****************************************************************
	# Volatility Position Sizing - ATR
	#****************************************************************** 
	atr = bt.apply(data, function(x) ATR(HLC(x),20)[,'atr'])

	# position size in units = ((porfolio size * % of capital to risk)/(ATR*2)) 
	data$weight[] = NA
		capital = 100000

		# risk 2% of capital
		data$weight[] = (capital * 2/100) / (2 * atr)

		# make sure you are not committing more than 100%
		max.allocation = capital / prices
		data$weight[] = iif(data$weight > max.allocation, max.allocation,data$weight)

	models$buy.hold.2atr = bt.run(data, type='share', capital=capital)					

	#*****************************************************************
	# Create Report
	#****************************************************************** 	
	models = rev(models)

	plotbt.custom.report.part1(models)

	plotbt.custom.report.part2(models)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/05/plot1-small.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/05/plot2-small.png)

夏普和 DVR 对于新策略都更高，而回撤更低。

要查看此示例的完整源代码，请查看[github 上的 bt.test.r 中的 bt.position.sizing.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
