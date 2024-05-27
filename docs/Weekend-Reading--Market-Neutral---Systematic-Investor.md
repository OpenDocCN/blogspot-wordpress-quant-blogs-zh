<!--yml

category: 未分类

日期：2024-05-18 14:31:46

-->

# 周末阅读：市场中性 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2013/11/02/weekend-reading-market-neutral/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/11/02/weekend-reading-market-neutral/#0001-01-01)

[主页](https://systematicinvestor.wordpress.com/ "前往主页")

[回测](https://systematicinvestor.wordpress.com/category/backtesting/)

,

[投资组合构建](https://systematicinvestor.wordpress.com/category/portfolio-construction/)

,

[R](https://systematicinvestor.wordpress.com/category/r/)

> 周末阅读：市场中性

## 周末阅读：市场中性

我最近在 Mebane Faber 的[The Problem with Market Neutral (and an Answer)](http://www.mebanefaber.com/2013/10/30/the-problem-with-market-neutral-and-an-answer/)一文中发现了一个非常有趣的想法。今天我想展示如何使用[系统投资者工具箱（Systematic Investor Toolbox）](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)来测试这样的策略：

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
		ret = temp[[1]]$Mkt.RF + temp[[1]]$RF
		price = bt.apply.matrix(ret / 100, function(x) cumprod(1 + x))
	data$SPY = make.stock.xts( price )

	# load historical momentum returns
	temp = get.fama.french.data('10_Portfolios_Prior_12_2', periodicity = '',download = T, clean = T)		
		ret = temp[[1]]
		price = bt.apply.matrix(ret / 100, function(x) cumprod(1 + x))
	data$HI.MO = make.stock.xts( price$High )
	data$LO.MO = make.stock.xts( price$Low )

	# align dates
	bt.prep(data, align='remove.na')

	#*****************************************************************
	# Code Strategies
	#*****************************************************************	
	models = list()

	data$weight[] = NA
		data$weight$SPY[] = 1
	models$SPY = bt.run.share(data, clean.signal=T)

	data$weight[] = NA
		data$weight$HI.MO[] = 1
	models$HI.MO = bt.run.share(data, clean.signal=T)

	data$weight[] = NA
		data$weight$LO.MO[] = 1
	models$LO.MO = bt.run.share(data, clean.signal=T)

	data$weight[] = NA
		data$weight$HI.MO[] = 1
		data$weight$LO.MO[] = -1
	models$MKT.NEUTRAL = bt.run.share(data, clean.signal=F)

	#*****************************************************************
	# Modified MN
	# The modified strategy below starts 100% market neutral, and depending on the drawdown bucket 
	# will reduce the shorts all the way to zero once the market has declined by 50%
	# (in 20% steps for every 10% decline in stocks)
	#*****************************************************************	
	market.drawdown = -100 * compute.drawdown(data$prices$SPY)
		market.drawdown.10.step = 10 * floor(market.drawdown / 10)
		short.allocation = 100 - market.drawdown.10.step * 2
		short.allocation[ short.allocation < 0 ] = 0

	data$weight[] = NA
		data$weight$HI.MO[] = 1
		data$weight$LO.MO[] = -1 * short.allocation / 100
	models$Modified.MN = bt.run.share(data, clean.signal=F)

	#*****************************************************************
	# Create Report
	#*****************************************************************
	strategy.performance.snapshoot(models, T)

```

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/11/plot1.jpg)

Mebane，非常感谢您分享这个伟大的观察和行之有效的策略！我鼓励读者们尝试这个想法，并分享他们的发现。

如果您想集中精力进行多头操作，一个浮现的想法是不完全投资，比如 90%的分配，一旦市场出现 20%的回撤，就投资 100%，期望快速恢复。

要查看此示例的完整源代码，请查看[GitHub 上的 bt.test.r 中的 bt.mebanefaber.modified.mn.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
