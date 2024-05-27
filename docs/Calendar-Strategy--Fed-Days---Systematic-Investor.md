<!--yml

category: 未分类

date: 2024-05-18 14:29:54

-->

# 日历策略：联邦日 | 系统化投资者

> Source: [`systematicinvestor.wordpress.com/2014/05/06/calendar-strategy-fed-days/#0001-01-01`](https://systematicinvestor.wordpress.com/2014/05/06/calendar-strategy-fed-days/#0001-01-01)

**更新**：有人指出原文由于利用 prices > SMA(prices,100) 语句引入了前瞻偏差问题。在日历策略逻辑中，我没有使用通常的一天滞后，因为重要的日期是提前知道的。然而， prices > SMA(prices,100) 语句应该滞后一天。我更新了图表和源代码。

今天，我想接着[日历策略：到期日](https://systematicinvestor.wordpress.com/2014/05/03/calendar-strategy-option-expiry/)这篇文章。让我们来检验[联邦储备会议日](http://www.federalreserve.gov/monetarypolicy/fomccalendars.htm)的重要性，如[联邦储备日和中期高点](http://quantifiableedges.blogspot.ca/search/label/Fed%20Study)文章中所述。

让我们深入研究，并检验[联邦储备会议日](http://www.federalreserve.gov/monetarypolicy/fomccalendars.htm)期间 SPY 的历史表现：

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

	tickers = spl('SPY')

	data <- new.env()
	getSymbols.extra(tickers, src = 'yahoo', from = '1980-01-01', env = data, set.symbolnames = T, auto.assign = T)
		for(i in data$symbolnames) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)
	bt.prep(data, align='keep.all', fill.gaps = T)

	#*****************************************************************
	# Setup
	#*****************************************************************
	prices = data$prices
		n = ncol(prices)

	dates = data$dates	

	models = list()

	universe = prices > 0
		# 100 day SMA filter
		universe = universe & prices > SMA(prices,100)

	# Find Fed Days
	info = get.FOMC.dates(F)
		key.date.index = na.omit(match(info$day, dates))

	key.date = NA * prices
		key.date[key.date.index,] = T

	#*****************************************************************
	# Strategy
	#*****************************************************************
	signals = list(T0=0)
		for(i in 1:15) signals[[paste0('N',i)]] = 0:i	
	signals = calendar.signal(key.date, signals)
	models = calendar.strategy(data, signals, universe = universe)

	strategy.performance.snapshoot(models, T, sort.performance=F)

```

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/05/plot12.png)

请注意上方的 100 天移动平均线滤镜。如果我们取消它，表现会明显下降。

```

	# custom stats	
	out = sapply(models, function(x) list(
		CAGR = 100*compute.cagr(x$equity),
		MD = 100*compute.max.drawdown(x$equity),
		Win = x$trade.summary$stats['win.prob', 'All'],
		Profit = x$trade.summary$stats['profitfactor', 'All']
		))	
	performance.barchart.helper(out, sort.performance = F)

	strategy.performance.snapshoot(models$N15, control=list(main=T))

	last.trades(models$N15)

	trades = models$N15$trade.summary$trades
		trades = make.xts(parse.number(trades[,'return']), as.Date(trades[,'entry.date']))
	layout(1:2)
		par(mar = c(4,3,3,1), cex = 0.8) 
	barplot(trades, main='N15 Trades', las=1)
	plot(cumprod(1+trades/100), type='b', main='N15 Trades', las=1)

```

**N15 策略：**

![plot2](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/05/plot22.png)

![plot3](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/05/plot32.png)

![plot4](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/05/plot42.png)

![plot5](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/05/plot52.png)

通过这篇文章，我想展示如何利用[系统化投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)轻松研究日历策略的表现。

接下来，我将研究[红利](http://en.wikipedia.org/wiki/Dividend)日的重要性。

要查看此示例的完整源代码，请查看[github 上的 bt.calendar.strategy.fed.days.test()函数的 bt.test.r](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
