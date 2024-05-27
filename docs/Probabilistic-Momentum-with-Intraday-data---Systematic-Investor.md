请注意，以下是源代码注释，不会被翻译：

类别：未分类

日期：2024-05-18 14:30:35

请注意，以下是源代码注释，不会被翻译：

# 基于日内数据的概率动量 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2014/03/31/probabilistic-momentum-with-intraday-data/#0001-01-01`](https://systematicinvestor.wordpress.com/2014/03/31/probabilistic-momentum-with-intraday-data/#0001-01-01)

我想跟进[日内数据](https://systematicinvestor.wordpress.com/2014/03/10/intraday-data/)帖子，测试在日内数据上[概率动量](https://systematicinvestor.wordpress.com/2014/02/17/probabilistic-momentum/)策略的表现。我将使用来自[Bonnot Gang](http://thebonnotgang.com/tbg/historical-data/)的 SPY 和 GLD 的日内数据来测试[策略](https://systematicinvestor.wordpress.com/2014/02/17/probabilistic-momentum/)。

```

##############################################################################
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

	# data from http://thebonnotgang.com/tbg/historical-data/
	# please save SPY and GLD 1 min data at the given path
	spath = 'c:/Desktop/'
	data = bt.load.thebonnotgang.data('SPY,GLD', spath)

	data1 <- new.env()		
		data1$FI = data$GLD
		data1$EQ = data$SPY
	data = data1
	bt.prep(data, align='keep.all', fill.gaps = T)

	lookback.len = 120
	confidence.level = 60/100

	prices = data$prices
		ret = prices / mlag(prices) - 1 

	models = list()

	#*****************************************************************
	# Simple Momentum
	#****************************************************************** 
	momentum = prices / mlag(prices, lookback.len)
	data$weight[] = NA
		data$weight$EQ[] = momentum$EQ > momentum$FI
		data$weight$FI[] = momentum$EQ <= momentum$FI
	models$Simple  = bt.run.share(data, clean.signal=T) 	

	#*****************************************************************
	# Probabilistic Momentum + Confidence Level
	# http://cssanalytics.wordpress.com/2014/01/28/are-simple-momentum-strategies-too-dumb-introducing-probabilistic-momentum/
	# http://cssanalytics.wordpress.com/2014/02/12/probabilistic-momentum-spreadsheet/
	#****************************************************************** 
	ir = sqrt(lookback.len) * runMean(ret$EQ - ret$FI, lookback.len) / runSD(ret$EQ - ret$FI, lookback.len)
	momentum.p = pt(ir, lookback.len - 1)

	data$weight[] = NA
		data$weight$EQ[] = iif(cross.up(momentum.p, confidence.level), 1, iif(cross.dn(momentum.p, (1 - confidence.level)), 0,NA))
		data$weight$FI[] = iif(cross.dn(momentum.p, (1 - confidence.level)), 1, iif(cross.up(momentum.p, confidence.level), 0,NA))
	models$Probabilistic  = bt.run.share(data, clean.signal=T) 	

	data$weight[] = NA
		data$weight$EQ[] = iif(cross.up(momentum.p, confidence.level), 1, iif(cross.up(momentum.p, (1 - confidence.level)), 0,NA))
		data$weight$FI[] = iif(cross.dn(momentum.p, (1 - confidence.level)), 1, iif(cross.up(momentum.p, confidence.level), 0,NA))
	models$Probabilistic.Leverage = bt.run.share(data, clean.signal=T) 	

	#*****************************************************************
	# Create Report
	#******************************************************************        
	strategy.performance.snapshoot(models, T)    

```

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/03/plot11.png)

接下来，让我们检查一下[策略](https://systematicinvestor.wordpress.com/2014/02/17/probabilistic-momentum/)每小时的性能。

```

	#*****************************************************************
	# Hourly Performance
	#******************************************************************    
	strategy.name = 'Probabilistic.Leverage'
	ret = models[[strategy.name]]$ret	
		ret.number = 100*as.double(ret)

	dates = index(ret)
	factor = format(dates, '%H')

	layout(1:2)
	par(mar=c(4,4,1,1))
	boxplot(tapply(ret.number, factor, function(x) x),outline=T, main=paste(strategy.name, 'Distribution of Returns'), las=1)
	barplot(tapply(ret.number, factor, function(x) sum(x)), main=paste(strategy.name, 'P&L by Hour'), las=1)

```

![plot2](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/03/plot21.png)

由于大的隔夜回报，9:30-10:00am 箱中的异常回报很多。也就是说，从今日开盘到昨日收盘的回报。如果我们每天排除这个观察结果，每个小时的分布会更一致。

```

   	#*****************************************************************
   	# Hourly Performance: Remove first return of the day (i.e. overnight)
   	#******************************************************************    
   	day.stat = bt.intraday.day(dates)
	ret.number[day.stat$day.start] = 0

   	layout(1:2)
   	par(mar=c(4,4,1,1))
	boxplot(tapply(ret.number, factor, function(x) x),outline=T, main=paste(strategy.name, 'Distribution of Returns'), las=1)
	barplot(tapply(ret.number, factor, function(x) sum(x)), main=paste(strategy.name, 'P&L by Hour'), las=1)

```

![plot3](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/03/plot31.png)

该[策略](https://systematicinvestor.wordpress.com/2014/02/17/probabilistic-momentum/)在上午表现最佳，下午和夜间逐渐减弱。

这些每小时的季节性图表只是分析基于日内数据策略表现的不同方式。

要查看此示例的完整源代码，请查看 github 上的 [bt.strategy.intraday.thebonnotgang.test() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
