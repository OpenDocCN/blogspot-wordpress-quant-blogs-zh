<!--yml

类别：未分类

时间：2024-05-18 14:31:04

-->

# 周末阅读：F-Squared | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2013/12/07/weekend-reading-f-squared/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/12/07/weekend-reading-f-squared/#0001-01-01)

Mebane Faber 发布了另一篇有趣的博客文章：[构建一个简单的行业轮动策略，基于动量和趋势](http://www.mebanefaber.com/2013/12/04/square-root-of-f-squared/)，引起了我的兴趣。今天我想展示如何使用[Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)来测试这样的策略：

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

	data = new.env()
	# load historical market returns
	temp = get.fama.french.data('F-F_Research_Data_Factors', periodicity = '',download = T, clean = T)
		ret = cbind(temp[[1]]$Mkt.RF + temp[[1]]$RF, temp[[1]]$RF)
		price = bt.apply.matrix(ret / 100, function(x) cumprod(1 + x))
	data$SPY = make.stock.xts( price$Mkt.RF )
	data$SHY = make.stock.xts( price$RF )

	# load historical sector returns
	temp = get.fama.french.data('10_Industry_Portfolios', periodicity = '',download = T, clean = T)		
		ret = temp[[1]]
		price = bt.apply.matrix(ret[,1:9] / 100, function(x) cumprod(1 + x))
	for(n in names(price)) data[[n]] = make.stock.xts( price[,n] )

	# align dates
	data$symbolnames = c(names(price), 'SHY', 'SPY')
	bt.prep(data, align='remove.na', dates='2000::')

	# back-test dates
	bt.dates = '2001:04::'

	#*****************************************************************
	# Setup
	#****************************************************************** 	
	prices = data$prices  
	n = ncol(data$prices)

	models = list()

	#*****************************************************************
	# Benchmark Strategies
	#****************************************************************** 			
	data$weight[] = NA
		data$weight$SPY[1] = 1
	models$SPY = bt.run.share(data, clean.signal=F, dates=bt.dates)

	weight = prices
		weight$SPY = NA
		weight$SHY = NA

	data$weight[] = NA
		data$weight[] = ntop(weight[], n)
	models$EW = bt.run.share(data, clean.signal=F, dates=bt.dates)

	#*****************************************************************
	# Code Strategies
	# http://www.mebanefaber.com/2013/12/04/square-root-of-f-squared/
	#****************************************************************** 			
	sma = bt.apply.matrix(prices, SMA, 10)

	# create position score
	position.score = sma
	position.score[ prices < sma ] = NA
		position.score$SHY = NA	
		position.score$SPY = NA	

	# equal weight allocation
	weight = ntop(position.score[], n)	

	# number of invested funds
	n.selected = rowSums(weight != 0)

	# cash logic
	weight$SHY[n.selected == 0,] = 1

	weight[n.selected == 1,] = 0.25 * weight[n.selected == 1,]
	weight$SHY[n.selected == 1,] = 0.75

	weight[n.selected == 2,] = 0.5 * weight[n.selected == 2,]
	weight$SHY[n.selected == 2,] = 0.5

	weight[n.selected == 3,] = 0.75 * weight[n.selected == 3,]
	weight$SHY[n.selected == 3,] = 0.25

	# cbind(round(100*weight,0), n.selected)	

	data$weight[] = NA
		data$weight[] = weight
	models$strategy1 = bt.run.share(data, clean.signal=F, dates=bt.dates)	

	#*****************************************************************
	# Create Report
	#******************************************************************       	
	strategy.performance.snapshoot(models, one.page = T)

```

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/12/plot11.png)

Mebane，非常感谢你分享你的好想法。我鼓励读者尝试这种策略，并回报结果。

请注意，我使用月度观察结果对这种策略进行了回测。使用月度数据，策略的最大回撤约为 17%。如果我们切换到每日数据，策略的最大回撤将达到 22%。2002 年有一个非常糟糕的月份。

要查看此示例的完整源代码，请查看[GitHub 上的 bt.test.r 中的 bt.mebanefaber.f.squared.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
