<!--yml
category: 未分类
date: 2024-05-18 14:41:04
-->

# Volatility Position Sizing to improve Risk Adjusted Performance | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2012/05/01/volatility-position-sizing-to-improve-risk-adjusted-performance/#0001-01-01](https://systematicinvestor.wordpress.com/2012/05/01/volatility-position-sizing-to-improve-risk-adjusted-performance/#0001-01-01)

[Home](https://systematicinvestor.wordpress.com/ "Go to homepage")

>

[Backtesting](https://systematicinvestor.wordpress.com/category/backtesting/)

,

[Portfolio Construction](https://systematicinvestor.wordpress.com/category/portfolio-construction/)

,

[R](https://systematicinvestor.wordpress.com/category/r/)

,

[Strategy](https://systematicinvestor.wordpress.com/category/strategy/)

,

[Trading Strategies](https://systematicinvestor.wordpress.com/category/trading-strategies/)

> Volatility Position Sizing to improve Risk Adjusted Performance

## Volatility Position Sizing to improve Risk Adjusted Performance

Today I want to show how to use Volatility Position Sizing to improve strategy’s Risk Adjusted Performance. I will use the [Average True Range (ATR)](http://stockcharts.com/school/doku.php?id=chart_school:technical_indicators:average_true_range_atr) as a measure of Volatility and will increase allocation during low Volatility periods and will decrease allocation during high Volatility periods. Following are two good references that explain these strategy in detail:

First, let’s load prices for SPY and compute Buy & Hold performance using the [Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/):

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
	tickers = spl('SPY')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)			
	bt.prep(data, align='keep.all', dates='1970::')	

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 
	prices = data$prices   
	nperiods = nrow(prices)

	models = list()

	#*****************************************************************
	# Buy & Hold
	#****************************************************************** 
	data$weight[] = 0
		data$weight[] = 1
	models$buy.hold = bt.run.share(data, clean.signal=T)

```

Next, let’s modify Buy & Hold strategy to vary it’s allocation according to the [Average True Range (ATR)](http://stockcharts.com/school/doku.php?id=chart_school:technical_indicators:average_true_range_atr).

```

	#*****************************************************************
	# Volatility Position Sizing - ATR
	#****************************************************************** 
	atr = bt.apply(data, function(x) ATR(HLC(x),20)[,'atr'])

	# position size in units = ((porfolio size * % of capital to risk)/(ATR*2)) 
	data$weight[] = NA
		capital = 100000

		# risk 2% of capital
		data$weight[] = (capital * 2/100) / (2 * atr)

		# make sure you are not committing more than 100%
		max.allocation = capital / prices
		data$weight[] = iif(data$weight > max.allocation, max.allocation,data$weight)

	models$buy.hold.2atr = bt.run(data, type='share', capital=capital)					

	#*****************************************************************
	# Create Report
	#****************************************************************** 	
	models = rev(models)

	plotbt.custom.report.part1(models)

	plotbt.custom.report.part2(models)

```

[![](img/e2febb7d4091b365e09b30cb7ab7391a.png "plot1.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/05/plot1-small.png)

[![](img/310f6746ec648872b35d63592b9099e7.png "plot2.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/05/plot2-small.png)

The Sharpe and DVR are both higher for new strategy and draw-downs are lower.

To view the complete source code for this example, please have a look at the [bt.position.sizing.test() function in bt.test.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r).