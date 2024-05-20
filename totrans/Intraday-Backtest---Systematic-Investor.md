<!--yml
category: 未分类
date: 2024-05-18 14:40:56
-->

# Intraday Backtest | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2012/04/23/intraday-backtest/#0001-01-01](https://systematicinvestor.wordpress.com/2012/04/23/intraday-backtest/#0001-01-01)

I came across a free source of Intraday Forex data while reading [Forex Trading with R : Part 1](http://lifeanalytics.blogspot.com/2011/01/forex-trading-with-r-part-1.html) post. You can download either Daily or Hourly historical Forex data from the [FXHISTORICALDATA.COM](http://www.fxhistoricaldata.com/).

The outline of this post:

*   Download and Import Forex data
*   Reference and Plot Intraday data
*   Daily Backtest
*   Intraday Backtest

First,I created a [getSymbols.fxhistoricaldata() function in data.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/data.r) to download Forex data from the [FXHISTORICALDATA.COM](http://www.fxhistoricaldata.com/). Following code loads ‘EURUSD’ hourly data and creates a candle chart for 2012:03:06 from 10 to 21 hours using the [Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/):

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

[![](img/ba4d3e017975de88c7b4e98952ac62ac.png "plot1.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot1-small2.png)

We can reference Intraday data by specifying hours, minutes, and seconds in addition to year, month, and day. I.e. YYYY:MM:DD HH:MM:SS

Next, let’s combine Daily price for SPY and Intraday quotes for EURUSD in one chart.

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

[![](img/af92e31be3966fdefffa565443577b63.png "plot2.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot2-small2.png)

Next, let’s create a Daily Backtest by investing into [Currency Majors](http://en.wikipedia.org/wiki/Currency_pair): EUR/USD, USD/JPY, GBP/USD, AUD/USD, USD/CHF and USD/CAD. I will investigate an Equal Weight portfolio and Timing portfolio as explained in the [A Quantitative Approach to Tactical Asset Allocation by M. Faber (2006)](http://www.mebanefaber.com/timing-model/) paper.

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

[![](img/20e2d5262afdb043338f468f605e825b.png "plot3.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot3-small2.png)

[![](img/eb5fc0c67f48cea106e50ad185c291cf.png "plot4.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot4-small.png)

Next, let’s create an Intraday Backtest using the same strategies.

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

[![](img/a9b9a8600f308aeb538a9b11b6091af0.png "plot5.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot5-small.png)

[![](img/1d74ba35939369cd67a4f46edeef5132.png "plot6.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot6-small.png)

Please note that the code for the Daily Backtest and Intraday Backtest is identical except for the line where we download the data:

*   Daily Backtest:

    ```
    getSymbols.fxhistoricaldata(tickers, 'day', data, download=T)
    ```

*   Intraday Backtest:

    ```
    getSymbols.fxhistoricaldata(tickers, 'hour', data, download=T)
    ```

It is easy to work with Intraday data and it is easy to create Intraday Backtest, right?

To view the complete source code for this example, please have a look at the [bt.intraday.test() function in bt.test.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r).