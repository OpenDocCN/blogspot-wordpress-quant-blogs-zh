<!--yml

类别：未分类

日期：2024 年 05 月 18 日 14:40:15

-->

# 波动率仓位调整 2 | 系统性投资者

> 来源：[`systematicinvestor.wordpress.com/2012/06/12/volatility-position-sizing-2/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/06/12/volatility-position-sizing-2/#0001-01-01)

我在 [波动率仓位调整以改善风险调整绩效](https://systematicinvestor.wordpress.com/2012/05/01/volatility-position-sizing-to-improve-risk-adjusted-performance/) 文章中讨论了使用 [真实波动范围 (ATR)](http://stockcharts.com/school/doku.php?id=chart_school:technical_indicators:average_true_range_atr) 作为波动率衡量的波动率仓位调整。

今天我想展示如何使用历史波动率调整投资组合杠杆。我们从使用 SPY 的买入并持有策略开始，并将其重新缩放为目标波动率为 10%。我将使用一个 60 天滚动的历史波动率来调整投资组合杠杆，以便将年度波动率定位为 10%。

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)
# https://systematicinvestor.wordpress.com/systematic-investor-toolbox/
###############################################################################
setInternet2(TRUE)
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')	
	tickers = 'SPY'

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)		
	bt.prep(data, align='keep.all', dates='1994::')

	#*****************************************************************
	# Buy and Hold
	#****************************************************************** 
	prices = data$prices
	models = list()

	data$weight[] = 1
	models$buy.hold = bt.run.share(data, clean.signal=T)

	#*****************************************************************
	# Buy and Hold with target 10% Volatility
	#****************************************************************** 
	ret.log = bt.apply.matrix(data$prices, ROC, type='continuous')
	hist.vol = sqrt(252) * bt.apply.matrix(ret.log, runSD, n = 60)

	data$weight[] = 0.1 / hist.vol
	models$buy.hold.volatility.weighted = bt.run.share(data, clean.signal=T)

	#*****************************************************************
	# Buy and Hold with target 10% Volatility and Max Total leverage 100%
	#****************************************************************** 		
	data$weight[] = 0.1 / hist.vol
		rs = rowSums(data$weight)
		data$weight[] = data$weight / iif(rs > 1, rs, 1) 			
	models$buy.hold.volatility.weighted.100 = bt.run.share(data, clean.signal=T)

	#*****************************************************************
	# Same, rebalanced Monthly
	#****************************************************************** 
	period.ends = endpoints(prices, 'months')
		period.ends = period.ends[period.ends > 0]

	data$weight[] = NA
	data$weight[period.ends,] = 0.1 / hist.vol[period.ends,]
		rs = rowSums(data$weight[period.ends,])
		data$weight[period.ends,] = data$weight[period.ends,] / iif(rs > 1, rs, 1) 			
	models$buy.hold.volatility.weighted.100.monthly = bt.run.share(data, clean.signal=T)

	#*****************************************************************
	# Create Report
	#****************************************************************** 
	# Plot perfromance
	plotbt(models, plotX = T, log = 'y', LeftMargin = 3)	    	
		mtext('Cumulative Performance', side = 2, line = 1)

	plotbt.custom.report.part2(rev(models))

	# Plot Portfolio Turnover for each strategy
	layout(1)
	barplot.with.labels(sapply(models, compute.turnover, data), 'Average Annual Portfolio Turnover', plotX = F, label='both')

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/06/plot1-small1.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/06/plot2-small1.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/06/plot3-small.png)

所有策略都很好地将投资组合杠杆重新缩放到目标 10%的波动率。

接下来我们来研究其他波动率指标。 [TTR](http://cran.r-project.org/web/packages/TTR/index.html) 包中的波动率函数包括以下波动率计算类型：

+   历史波动率

+   加曼和克拉斯

+   帕金森

+   罗杰斯和萨切尔

+   加曼和克拉斯 – 杨和张

+   杨和张

我们可以很容易地修改上述算法以使用这些不同的波动率计算方法。我最喜欢 [R](http://www.r-project.org/) 的一点是，你可以想象到的任何东西都有相应的函数或包 🙂

```

	#*****************************************************************
	# Next let's examine other volatility measures
	#****************************************************************** 
	models = models[c('buy.hold' ,'buy.hold.volatility.weighted.100.monthly')]

	# TTR volatility calc types
	calc = c("close", "garman.klass", "parkinson", "rogers.satchell", "gk.yz", "yang.zhang")

	ohlc = OHLC(data$SPY)
	for(icalc in calc) {
		vol = volatility(ohlc, calc = icalc, n = 60, N = 252)

		data$weight[] = NA
		data$weight[period.ends,] = 0.1 / vol[period.ends,]
			rs = rowSums(data$weight[period.ends,])
			data$weight[period.ends,] = data$weight[period.ends,] / iif(rs > 1, rs, 1) 			
		models[[icalc]] = bt.run.share(data, clean.signal=T)
	}

	#*****************************************************************
	# Create Report
	#****************************************************************** 
	# Plot performance
	plotbt(models, plotX = T, log = 'y', LeftMargin = 3)	    	
		mtext('Cumulative Performance', side = 2, line = 1)

	plotbt.strategy.sidebyside(models)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/06/plot4-small.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/06/plot5-small.png)

简单的历史波动率在定位波动率和控制回撤方面做得最好。

接下来让我们将波动率仓位调整的思想应用到策略的权益曲线上。

```

	#*****************************************************************
	# Volatility Position Sizing applied to MA cross-over strategy's Equity Curve
	#****************************************************************** 
	models = list()	

	sma.fast = SMA(prices, 50)
	sma.slow = SMA(prices, 200)
	weight = iif(sma.fast >= sma.slow, 1, -1)

	data$weight[] = weight
	models$ma.crossover = bt.run.share(data, clean.signal=T)

	#*****************************************************************
	# Target 10% Volatility
	#****************************************************************** 
	ret.log = bt.apply.matrix(models$ma.crossover$equity, ROC, type='continuous')
	hist.vol = sqrt(252) * bt.apply.matrix(ret.log, runSD, n = 60)

	data$weight[] = NA
		data$weight[period.ends,] = (0.1 / hist.vol[period.ends,]) * weight[period.ends,]
		# limit total leverage to 100%		
		rs = rowSums(data$weight[period.ends,])
		data$weight[period.ends,] = data$weight[period.ends,] / iif(abs(rs) > 1, abs(rs), 1) 			
	models$ma.crossover.volatility.weighted.100.monthly = bt.run.share(data, clean.signal=T)

	#*****************************************************************
	# Create Report
	#****************************************************************** 
	# Plot perfromance
	plotbt(models, plotX = T, log = 'y', LeftMargin = 3)	    	
		mtext('Cumulative Performance', side = 2, line = 1)

	plotbt.custom.report.part2(rev(models))

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/06/plot6-small.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/06/plot7-small.png)

波动率仓位调整确实可以使策略的波动率接近目标 10%的波动率。

在最终的示例中，我将应用于 M. Faber 开发的 Timing 策略的波动率仓位调整。

```

	#*****************************************************************
	# Apply Volatility Position Sizing Timing stretegy by M. Faber
	#****************************************************************** 
	tickers = spl('SPY,QQQ,EEM,IWM,EFA,TLT,IYR,GLD')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)		
	bt.prep(data, align='remove.na', dates='1994::')

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 
	prices = data$prices   
		n = ncol(prices)
	models = list()

	period.ends = endpoints(prices, 'months')
		period.ends = period.ends[period.ends > 0]

	#*****************************************************************
	# Equal Weight
	#****************************************************************** 
	data$weight[] = NA
		data$weight[period.ends,] = ntop(prices[period.ends,], n)
		data$weight[1:200,] = NA
	models$equal.weight = bt.run.share(data, clean.signal=F)

	#*****************************************************************
	# Timing by M. Faber
	#****************************************************************** 
	sma = bt.apply.matrix(prices, SMA, 200)

	weight = ntop(prices, n) * (prices > sma)
	data$weight[] = NA
		data$weight[period.ends,] = weight[period.ends,]
	models$timing = bt.run.share(data, clean.signal=F)

	#*****************************************************************
	# Timing with target 10% Volatility
	#****************************************************************** 
	ret.log = bt.apply.matrix(models$timing$equity, ROC, type='continuous')
	hist.vol = bt.apply.matrix(ret.log, runSD, n = 60)
		hist.vol = sqrt(252) * as.vector(hist.vol)

	data$weight[] = NA
		data$weight[period.ends,] = (0.1 / hist.vol[period.ends]) * weight[period.ends,]
		rs = rowSums(data$weight)
		data$weight[] = data$weight / iif(rs > 1, rs, 1) 				
		data$weight[1:200,] = NA
	models$timing.volatility.weighted.100.monthly = bt.run.share(data, clean.signal=T)

	#*****************************************************************
	# Create Report
	#****************************************************************** 
	# Plot perfromance
	plotbt(models, plotX = T, log = 'y', LeftMargin = 3)	    	
		mtext('Cumulative Performance', side = 2, line = 1)

	plotbt.custom.report.part2(rev(models))

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/06/plot8-small.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/06/plot9-small.png)

波动率仓位调整是许多仓位调整算法之一，可以成为您的资金管理规则的一部分。让我知道哪种仓位调整方案对您最有效。

要查看此示例的完整源代码，请查看[github 上的 bt.volatility.position.sizing.test()函数的 bt.test.r](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
