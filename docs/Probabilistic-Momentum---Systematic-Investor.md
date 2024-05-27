<!--yml

类别：未分类

日期：2024-05-18 14:30:56

-->

# 概率动量 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2014/02/17/probabilistic-momentum/#0001-01-01`](https://systematicinvestor.wordpress.com/2014/02/17/probabilistic-momentum/#0001-01-01)

[David Varadi](http://cssanalytics.wordpress.com)最近讨论了一个有趣的策略

[简单动量策略太愚蠢了吗？介绍概率动量](http://cssanalytics.wordpress.com/2014/01/28/are-simple-momentum-strategies-too-dumb-introducing-probabilistic-momentum/)帖子。如果您有兴趣在 Excel 中进行计算，David 还提供了[概率动量电子表格](http://cssanalytics.wordpress.com/2014/02/12/probabilistic-momentum-spreadsheet/)。今天我想展示如何使用[Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)测试这样的策略：

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

	tickers = spl('SPY,TLT')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)
	bt.prep(data, align='remove.na', dates='2005::')

	#*****************************************************************
	# Setup
	#****************************************************************** 
	lookback.len = 60

	prices = data$prices

	models = list()

	#*****************************************************************
	# Simple Momentum
	#****************************************************************** 
	momentum = prices / mlag(prices, lookback.len)
	data$weight[] = NA
		data$weight$SPY[] = momentum$SPY > momentum$TLT
		data$weight$TLT[] = momentum$SPY <= momentum$TLT
	models$Simple  = bt.run.share(data, clean.signal=T) 	

```

简单动量策略如果 SPY 的动量大于 TLT 的动量，则投资于 SPY，否则投资于 TLT。

```

	#*****************************************************************
	# Probabilistic Momentum
	#****************************************************************** 
	confidence.level = 60/100
	ret = prices / mlag(prices) - 1 

	ir = sqrt(lookback.len) * runMean(ret$SPY - ret$TLT, lookback.len) / runSD(ret$SPY - ret$TLT, lookback.len)
	momentum.p = pt(ir, lookback.len - 1)

	data$weight[] = NA
		data$weight$SPY[] = iif(cross.up(momentum.p, confidence.level), 1, iif(cross.dn(momentum.p, (1 - confidence.level)), 0,NA))
		data$weight$TLT[] = iif(cross.dn(momentum.p, (1 - confidence.level)), 1, iif(cross.up(momentum.p, confidence.level), 0,NA))
	models$Probabilistic  = bt.run.share(data, clean.signal=T) 	

```

[概率动量](http://cssanalytics.wordpress.com/2014/01/28/are-simple-momentum-strategies-too-dumb-introducing-probabilistic-momentum/)策略使用概率动量度量和置信水平来决定分配。如果 SPY vs TLT 的[概率动量](http://cssanalytics.wordpress.com/2014/01/28/are-simple-momentum-strategies-too-dumb-introducing-probabilistic-momentum/)高于置信水平，则策略投资于 SPY，如果 SPY vs TLT 的[概率动量](http://cssanalytics.wordpress.com/2014/01/28/are-simple-momentum-strategies-too-dumb-introducing-probabilistic-momentum/)低于 1-置信水平，则投资于 TLT。

为了使策略更具吸引力，我增加了一种可以将 SPY 分配提高 50%的版本

```

	#*****************************************************************
	# Probabilistic Momentum + SPY Leverage 
	#****************************************************************** 
	data$weight[] = NA
		data$weight$SPY[] = iif(cross.up(momentum.p, confidence.level), 1, iif(cross.up(momentum.p, (1 - confidence.level)), 0,NA))
		data$weight$TLT[] = iif(cross.dn(momentum.p, (1 - confidence.level)), 1, iif(cross.up(momentum.p, confidence.level), 0,NA))
	models$Probabilistic.Leverage = bt.run.share(data, clean.signal=T) 	

	#*****************************************************************
	# Create Report
	#******************************************************************    
	strategy.performance.snapshoot(models, T)

```

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/02/plot1.png)

回测结果看起来与[简单动量策略太愚蠢了吗？介绍概率动量](http://cssanalytics.wordpress.com/2014/01/28/are-simple-momentum-strategies-too-dumb-introducing-probabilistic-momentum/)帖子中报告的结果非常相似。

但是，我无法精确地重现过渡图。看起来我的解释会产生更多的顿挫。

```

	#*****************************************************************
	# Visualize Signal
	#******************************************************************        
	cols = spl('steelblue1,steelblue')
	prices = scale.one(data$prices)

	layout(1:3)

	plota(prices$SPY, type='l', ylim=range(prices), plotX=F, col=cols[1], lwd=2)
	plota.lines(prices$TLT, type='l', plotX=F, col=cols[2], lwd=2)
		plota.legend('SPY,TLT',cols,as.list(prices))

	highlight = models$Probabilistic$weight$SPY > 0
		plota.control$col.x.highlight = iif(highlight, cols[1], cols[2])
	plota(models$Probabilistic$equity, type='l', plotX=F, x.highlight = highlight | T)
		plota.legend('Probabilistic,SPY,TLT',c('black',cols))

	highlight = models$Simple$weight$SPY > 0
		plota.control$col.x.highlight = iif(highlight, cols[1], cols[2])
	plota(models$Simple$equity, type='l', plotX=T, x.highlight = highlight | T)
		plota.legend('Simple,SPY,TLT',c('black',cols))	

```

![plot2](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/02/plot2.png)

[David](http://cssanalytics.wordpress.com)非常感谢您分享的好想法。我鼓励读者尝试这个策略并反馈。

要查看此示例的完整源代码，请查看[github 上的 bt.test.r 中的 bt.probabilistic.momentum.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
