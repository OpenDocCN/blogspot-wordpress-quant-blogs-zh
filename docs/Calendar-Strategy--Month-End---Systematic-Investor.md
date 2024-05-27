<!--yml

category: 未分类

日期：2024-05-18 14:30:10

-->

# 日历策略：月底 | 系统化投资者

> 来源：[`systematicinvestor.wordpress.com/2014/04/28/calendar-strategy-month-end/#0001-01-01`](https://systematicinvestor.wordpress.com/2014/04/28/calendar-strategy-month-end/#0001-01-01)

日历策略是一个非常简单的策略，它在预先知道的日期进行买入和卖出。今天我想展示如何轻松地调查在月底附近的绩效。

首先，让我们加载来自 Yahoo Finance 的 SPY 的历史价格，并计算月底的 SPY 绩效。即策略将在 30 日收盘时开启多头仓位，并在 31 日收盘时平仓。

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

	models = list()

	period.ends = date.month.ends(data$dates, F)

	#*****************************************************************
	# Strategy
	#*****************************************************************
	key.date = NA * prices
		key.date[period.ends] = T

	universe = prices > 0
	signal = key.date

	data$weight[] = NA
		data$weight[] = ifna(universe & key.date, F)
	models$T0 = bt.run.share(data, do.lag = 0, trade.summary=T, clean.signal=T) 

```

请注意，在上述的 bt.run.share 调用中，我将 do.lag 参数设置为零（do.lag 参数的默认值为一）。将默认设置为一的原因是因为信号（交易决策）是使用当天所有可用信息推导出的，所以仓位只能在下一天实施。即

```
portfolio.returns = lag(signal, do.lag) * returns = lag(signal, 1) * returns
```

但是，在日历策略中，没有必要延迟信号，因为交易日是预先知道的。即

```
portfolio.returns = lag(signal, do.lag) * returns = signal * returns
```

接下来，我创建了两个函数来帮助信号创建和策略测试：

```

	calendar.strategy <- function(data, signal, universe = data$prices > 0) {
		data$weight[] = NA
			data$weight[] = ifna(universe & signal, F)
		bt.run.share(data, do.lag = 0, trade.summary=T, clean.signal=T)  	
	}

	calendar.signal <- function(key.date, offsets = 0) {
		signal = mlag(key.date, offsets[1])
		for(i in offsets) signal = signal | mlag(key.date, i)
		signal
	}

	# Trade on key.date
	models$T0 = calendar.strategy(data, key.date)

	# Trade next day after key.date
	models$N1 = calendar.strategy(data, mlag(key.date,1))
	# Trade two days next(after) key.date
	models$N2 = calendar.strategy(data, mlag(key.date,2))

	# Trade a day prior to key.date
	models$P1 = calendar.strategy(data, mlag(key.date,-1))
	# Trade two days prior to key.date
	models$P2 = calendar.strategy(data, mlag(key.date,-2))

	# Trade: open 2 days before the key.date and close 2 days after the key.date
	signal = key.date | mlag(key.date,-1) | mlag(key.date,-2) | mlag(key.date,1) | mlag(key.date,2)
	models$P2N2 = calendar.strategy(data, signal)

	# same, but using helper function above	
	models$P2N2 = calendar.strategy(data, calendar.signal(key.date, -2:2))

	strategy.performance.snapshoot(models, T)

	strategy.performance.snapshoot(models, control=list(comparison=T), sort.performance=F)

```

上面，T0 是一个日历策略，它在 30 日买入，31 日卖出。即仅在月底持有仓位。P1 和 P2 是两种分别在前一天和前两天买入的策略。N1 和 N2 是两种分别在后一天和后两天买入的策略。

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/04/plot11.png)

![plot2](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/04/plot21.png)

N1 策略，即在 31 日买入，次月 1 日卖出，似乎对 SPY 最有效。

最后，让我们看看实际交易情况：

```

	last.trades <- function(model, n=20, make.plot=T, return.table=F) {
		ntrades = min(n, nrow(model$trade.summary$trades))		
		trades = last(model$trade.summary$trades, ntrades)
		if(make.plot) {
			layout(1)
			plot.table(trades)
		}	
		if(return.table) trades	
	}

	last.trades(models$P2)

```

![plot3](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/04/plot3.png)

P2 策略在月底前 3 天收盘时进入仓位，并在月底前 2 天收盘时退出仓位。即绩效归因于仅在月底前 2 天的收益。

通过这篇文章，我想展示如何使用[系统化投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)轻松地研究日历策略的绩效。

接下来，我将展示日历策略在各种重要日期的应用。

要查看此示例的完整源代码，请查看[GitHub 上的 bt.test.r 中的 bt.calendar.strategy.month.end.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
