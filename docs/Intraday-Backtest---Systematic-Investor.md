<!--yml

分类：未分类

日期：2024-05-18 14:40:56

-->

# 日内回测 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/04/23/intraday-backtest/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/04/23/intraday-backtest/#0001-01-01)

在阅读[《用 R 进行外汇交易：第一部分》](http://lifeanalytics.blogspot.com/2011/01/forex-trading-with-r-part-1.html)帖子时，我找到了一个免费的外汇日内数据源。您可以从[FXHISTORICALDATA.COM](http://www.fxhistoricaldata.com/)下载每日或每小时的的历史外汇数据。

本帖大纲：

+   下载并导入外汇数据

+   引用并绘制日内数据

+   日回测

+   日内回测

首先，我在 github 上的[data.r](https://github.com/systematicinvestor/SIT/blob/master/R/data.r)中创建了一个[getSymbols.fxhistoricaldata()函数](https://github.com/systematicinvestor/SIT/blob/master/R/data.r)以从[FXHISTORICALDATA.COM](http://www.fxhistoricaldata.com/)下载外汇数据。以下代码加载了“EURUSD”的每小时数据，并使用[Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)创建了 2012 年 3 月 6 日从 10 点到 21 点的蜡烛图：

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)
# https://systematicinvestor.wordpress.com/systematic-investor-toolbox/
###############################################################################
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')	

	EURUSD = getSymbols.fxhistoricaldata('EURUSD', 'hour', auto.assign = F, download=T)
	SPY = getSymbols('SPY', src = 'yahoo', from = '1980-01-01', auto.assign = F)

	#*****************************************************************
	# Reference intraday period
	#****************************************************************** 
	plota(EURUSD['2012:03:06 10::2012:03:06 21'], type='candle', main='EURUSD on 2012:03:06 from 10 to 21')

```

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot1-small2.png)

我们可以通过指定年、月、日、时、分、秒来引用日内数据。即 YYYY:MM:DD HH:MM:SS。

接下来，让我们在同一个图表中将 SPY 的日价格和 EURUSD 的日内报价结合在一起。

```

	#*****************************************************************
	# Plot hourly and daily prices on the same chart
	#****************************************************************** 	
	# two Y axis plot	
	dates= '2012:01:01::2012:01:11'
	y = SPY[dates]
	plota(y, type = 'candle', LeftMargin=3)

	y = EURUSD[dates]
	plota2Y(y, ylim = range(OHLC(y), na.rm=T), las=1, col='red', col.axis = 'red')
		plota.ohlc(y, col=plota.candle.col(y))
	plota.legend('SPY(rhs),EURUSD(lhs)', 'black,red', list(SPY[dates],EURUSD[dates]))

```

![plot2.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot2-small2.png)

接下来，让我们通过投资[货币 majors](http://en.wikipedia.org/wiki/Currency_pair)：EUR/USD、USD/JPY、GBP/USD、AUD/USD、USD/CHF 和 USD/CAD 来创建一个日常回测。我将调查一个等权组合和时机组合，如[M. Faber 在《Tactical Asset Allocation 的定量方法》（2006 年）](http://www.mebanefaber.com/timing-model/)论文中所解释的。

```

	#*****************************************************************
	# Universe: Currency Majors
	# http://en.wikipedia.org/wiki/Currency_pair	
	#****************************************************************** 
	tickers = spl('EURUSD,USDJPY,GBPUSD,AUDUSD,USDCHF,USDCAD')

	#*****************************************************************
	# Daily Backtest
	#****************************************************************** 
	data <- new.env()
	getSymbols.fxhistoricaldata(tickers, 'day', data, download=T)
	bt.prep(data, align='remove.na', dates='1990::')

	prices = data$prices   
	n = len(tickers)  
	models = list()

	# Equal Weight
	data$weight[] = NA
		data$weight[] = ntop(prices, n)
	models$equal.weight = bt.run.share(data, clean.signal=F)

	# Timing by M. Faber
	sma = bt.apply.matrix(prices, SMA, 200)
	data$weight[] = NA
		data$weight[] = ntop(prices, n) * (prices > sma)
	models$timing = bt.run.share(data, clean.signal=F)

	# Report
	models = rev(models)
	plotbt.custom.report.part1(models)
	plotbt.custom.report.part2(models)

```

![plot3.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot3-small2.png)

![plot4.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot4-small.png)

接下来，让我们使用相同的策略创建一个日内回测。

```

	#*****************************************************************
	# Intraday Backtest
	#****************************************************************** 
	data <- new.env()	
	getSymbols.fxhistoricaldata(tickers, 'hour', data, download=T)	
	bt.prep(data, align='remove.na', dates='1990::')

	prices = data$prices   
	n = len(tickers)  
	models = list()

	# Equal Weight
	data$weight[] = NA
		data$weight[] = ntop(prices, n)
	models$equal.weight = bt.run.share(data, clean.signal=F)

	# Timing by M. Faber
	sma = bt.apply.matrix(prices, SMA, 200)
	data$weight[] = NA
		data$weight[] = ntop(prices, n) * (prices > sma)
	models$timing = bt.run.share(data, clean.signal=F)

	# Report
	models = rev(models)
	plotbt.custom.report.part1(models)
	plotbt.custom.report.part2(models)	

```

![plot5.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot5-small.png)

![plot6.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot6-small.png)

请注意，日常回测和日内回测的代码除下载数据的行外都相同：

+   日回测：

    ```
    getSymbols.fxhistoricaldata(tickers, 'day', data, download=T)
    ```

+   日内回测：

    ```
    getSymbols.fxhistoricaldata(tickers, 'hour', data, download=T)
    ```

使用日内数据很容易，并且很容易创建日内回测，对吧？

要查看此例子的完整源代码，请查看[bt.intraday.test()函数在 github 上的 bt.test.r 文件](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
