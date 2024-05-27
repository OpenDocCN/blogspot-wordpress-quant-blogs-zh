<!--yml

category: 未分类

date: 2024-05-18 14:30:02

-->

# 日历策略：期权到期 | 系统化投资者

> 来源：[`systematicinvestor.wordpress.com/2014/05/03/calendar-strategy-option-expiry/#0001-01-01`](https://systematicinvestor.wordpress.com/2014/05/03/calendar-strategy-option-expiry/#0001-01-01)

今天，我想继续讨论[日历策略：月末](https://systematicinvestor.wordpress.com/2014/04/28/calendar-strategy-month-end/)。让我们来看看期权到期日的表现，就像[The Mooost Wonderful Tiiiiiiime of the Yearrrrrrrrr!](http://quantifiableedges.blogspot.com/2011/12/mooost-wonderful-tiiiiiiime-of.html)中所述。

首先，我创建了两个方便的函数来创建日历信号和回测日历策略：calendar.signal 和 calendar.strategy 函数在[github 上的 strategy.r](https://github.com/systematicinvestor/SIT/blob/master/R/strategy.r)。

现在，让我们深入研究一下 12 月期权到期期间 SPY 的历史表现：

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

	# Find Friday before options expiration week in December
	years = date.year(range(dates))
	second.friday = third.friday.month(years[1]:years[2], 12) - 7
		key.date.index = na.omit(match(second.friday, dates))

	key.date = NA * prices
		key.date[key.date.index,] = T

	#*****************************************************************
	# Strategy: Op-ex week in December most bullish week of the year for the SPX
	#   Buy: December Friday prior to op-ex.
	#   Sell X days later: 100K/trade 1984-present
	# http://quantifiableedges.blogspot.com/2011/12/mooost-wonderful-tiiiiiiime-of.html
	#*****************************************************************
	signals = list(T0=0)
		for(i in 1:15) signals[[paste0('N',i)]] = 0:i	
	signals = calendar.signal(key.date, signals)
	models = calendar.strategy(data, signals, universe = universe)

	strategy.performance.snapshoot(models, T, sort.performance=F)

```

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/05/plot1.png)

策略表现各异，接下来让我们更详细地来看一下

```

	# custom stats	
	out = sapply(models, function(x) list(
		CAGR = 100*compute.cagr(x$equity),
		MD = 100*compute.max.drawdown(x$equity),
		Win = x$trade.summary$stats['win.prob', 'All'],
		Profit = x$trade.summary$stats['profitfactor', 'All']
		))	
	performance.barchart.helper(out, sort.performance = F)

	# Plot 15 day strategy
	strategy.performance.snapshoot(models$N15, control=list(main=T))

	# Plot trades for 15 day strategy
	last.trades(models$N15)

	# Make a summary plot of trades for 15 day strategy
	trades = models$N15$trade.summary$trades
		trades = make.xts(parse.number(trades[,'return']), as.Date(trades[,'entry.date']))
	layout(1:2)
		par(mar = c(4,3,3,1), cex = 0.8) 
	barplot(trades, main='Trades', las=1)
	plot(cumprod(1+trades/100), type='b', main='Trades', las=1)

```

**15 天策略的详情：**

![plot2](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/05/plot2.png)

![plot3](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/05/plot3.png)

![plot4](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/05/plot4.png)

![plot5](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/05/plot5.png)

通过这篇文章，我想展示如何轻松使用[系统化投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)来研究日历策略的表现。

接下来，我将重点关注[FED 会议](http://www.federalreserve.gov/monetarypolicy/fomccalendars.htm)日的重要性。

要查看此示例的完整源代码，请查看

[bt.calendar.strategy.option.expiry.test() 函数在 github 上的 bt.test.r](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
