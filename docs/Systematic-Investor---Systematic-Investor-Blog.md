<!--yml

类别：未分类

日期：2024-05-18 14:49:21

-->

# 系统投资者 | 系统投资者博客

> 来源：[`systematicinvestor.wordpress.com#0001-01-01`](https://systematicinvestor.wordpress.com#0001-01-01)

日历策略是一个非常简单的策略，它在预定的日子买入和卖出。今天我想展示我们如何轻松地研究在月底及其附近日期的表现。

首先，让我们从雅虎财经加载 SPY 的历史价格，并计算月底的 SPY 表现。即策略在 30 号收盘时买入，在 31 号收盘时卖出。

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

请注意，在上面的 bt.run.share 调用中，我将 do.lag 参数设置为零（do.lag 参数的默认值为一）。默认设置为一的原因是由于信号（交易决策）是使用今天可用的所有信息得出的，所以头寸只能在下一天实施。即

```
portfolio.returns = lag(signal, do.lag) * returns = lag(signal, 1) * returns
```

然而，在日历策略中，无需滞后信号，因为交易日期可以提前知道。即

```
portfolio.returns = lag(signal, do.lag) * returns = signal * returns
```

然后，我创建了两个函数来帮助生成信号和策略测试：

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

上面，T0 是一个在 30 号买入，在 31 号卖出的日历策略。即只在月底这一天持有头寸。P1 和 P2 是在前一天和前两天买入的两个策略。N1 和 N2 是在后一天和后两天买入的两个策略。

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/04/plot11.png)

![plot2](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/04/plot21.png)

N1 策略，在 31 号买入，在下一个月的 1 号卖出，似乎对 SPY 最有效。

最后，让我们看看实际交易：

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

P2 策略在月底前 3 天收盘时进入头寸，在月底前 2 天收盘时退出头寸。即表现仅由月底前 2 天的回报决定。

通过这篇文章，我想展示我们如何轻松地使用[系统投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)来研究日历策略的表现。

接下来，我将演示日历策略在各种重要日期的应用。

要查看这个示例的完整源代码，请查看 GitHub 上的[bt.calendar.strategy.month.end.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
