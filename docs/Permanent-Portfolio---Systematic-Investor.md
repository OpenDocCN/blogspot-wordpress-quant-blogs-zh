<!--yml

类别：未分类

日期：2024-05-18 14:37:51

-->

# 永久组合 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/09/18/permanent-portfolio/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/09/18/permanent-portfolio/#0001-01-01)

首先，快速更新：我将把 SIT 包的发布日期推迟几个月，可能在 11 月。

现在回到帖子。最近我在[GestaltU](http://gestaltu.blogspot.ca/)博客上发现了一系列关于[永久组合](http://gestaltu.blogspot.ca/2012/08/permanent-portfolio-shakedown-part-1.html)的有趣帖子。今天我想向您展示如何使用[系统投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)对[永久组合](http://en.wikipedia.org/wiki/Fail-Safe_Investing)进行回测。

简单的[永久组合](http://en.wikipedia.org/wiki/Fail-Safe_Investing)包括股票(SPY)、黄金(GLD)、国债(TLT)和现金(SHY)的等额分配。[每个 25%的分配]如果任何分配超出 15% – 35%的范围，则每年重新平衡一次投资组合。

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
	tickers = spl('SPY,TLT,GLD,SHY')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)

		# extend GLD with Gold.PM - London Gold afternoon fixing prices
		data$GLD = extend.GLD(data$GLD)

	bt.prep(data, align='remove.na')

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 		
	prices = data$prices   
		n = ncol(prices)
		nperiods = nrow(prices)

	# annual
	period.ends = endpoints(prices, 'years')
		period.ends = period.ends[period.ends > 0]		
		period.ends.y = c(1, period.ends)

	# quarterly
	period.ends = endpoints(prices, 'quarters')
		period.ends = period.ends[period.ends > 0]		
		period.ends.q = c(1, period.ends)

	models = list()

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 	
	target.allocation = matrix(rep(1/n,n), nrow=1)

	# Buy & Hold	
	data$weight[] = NA	
		data$weight[period.ends.y[1],] = target.allocation
	models$buy.hold = bt.run.share(data, clean.signal=F)

	# Equal Weight Annual
	data$weight[] = NA
		data$weight[period.ends.y,] = ntop(prices[period.ends.y,], n)
	models$equal.weight.y = bt.run.share(data, clean.signal=F)

	# Equal Weight Quarterly
	data$weight[] = NA
		data$weight[period.ends.q,] = ntop(prices[period.ends.q,], n)
	models$equal.weight.q = bt.run.share(data, clean.signal=F)

```

基于 10%的阈值进行再平衡（即投资组合权重超出 15% – 35%的范围）我将使用在[Backtesting Rebalancing methods](https://systematicinvestor.wordpress.com/2011/12/16/backtesting-rebalancing-methods/)文章中介绍的 bt.max.deviation.rebalancing()函数。

```

	#*****************************************************************
	# Rebalance based on threshold
	#****************************************************************** 	
	# Rebalance only when threshold is broken
	models$threshold.y = bt.max.deviation.rebalancing(data, models$buy.hold, target.allocation, 10/100, 0, period.ends = period.ends.y) 

	# Rebalance only when threshold is broken
	models$threshold.q = bt.max.deviation.rebalancing(data, models$buy.hold, target.allocation, 10/100, 0, period.ends = period.ends.q) 

	#*****************************************************************
	# Create Report
	#******************************************************************       
	plotbt.custom.report.part1(models)       

	plotbt.strategy.sidebyside(models)

	# Plot Portfolio Turnover for each Rebalancing method
	layout(1:2)
	barplot.with.labels(sapply(models, compute.turnover, data), 'Average Annual Portfolio Turnover', F)
	barplot.with.labels(sapply(models, compute.max.deviation, target.allocation), 'Maximum Deviation from Target Mix')

```

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/09/plot1-small1.png)

![plot2.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/09/plot2-small.png)

![plot3.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/09/plot3-small1.png)

使用 10%的阈值进行季度再平衡可以创建一个具有优异表现和低周转率的吸引人的投资组合。

要查看此例的完整源代码，请查看[github 上 bt.permanent.portfolio.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
