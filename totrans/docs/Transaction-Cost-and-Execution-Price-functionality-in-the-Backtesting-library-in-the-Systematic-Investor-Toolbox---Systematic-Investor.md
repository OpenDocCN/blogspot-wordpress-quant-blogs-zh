<!--yml
category: 未分类
date: 2024-05-18 14:41:33
-->

# Transaction Cost and Execution Price functionality in the Backtesting library in the Systematic Investor Toolbox | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2012/04/03/transaction-cost-and-execution-price-functionality-in-the-backtesting-library-in-the-systematic-investor-toolbox/#0001-01-01](https://systematicinvestor.wordpress.com/2012/04/03/transaction-cost-and-execution-price-functionality-in-the-backtesting-library-in-the-systematic-investor-toolbox/#0001-01-01)

I want to introduce the [Transaction Cost](http://en.wikipedia.org/wiki/Transaction_cost) and Execution Price functionality in the Backtesting library in the [Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/).

The Transaction Cost is implemented by a commission parameter in the bt.run() function. You may specify the commissions in $ per share for “share” type backtest and as a percentage of total trade for “weight” type backtest.

Following is a simple example of 50 / 200 day moving average cross over strategy with 10c per share commission:

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
		data$execution.price[] = NA
		data$weight[] = 1
	models$buy.hold = bt.run.share(data, clean.signal=T)

	#*****************************************************************
	# MA cross-over strategy
	#****************************************************************** 
	sma.fast = SMA(prices, 50)
	sma.slow = SMA(prices, 200)
		signal = iif(sma.fast >= sma.slow, 1, -1)

	data$weight[] = NA
		data$weight[] = signal
	models$ma.crossover = bt.run.share(data, clean.signal=T, trade.summary = TRUE)

	#*****************************************************************
	# MA cross-over strategy, add 10c per share commission
	#*****************************************************************	
	data$weight[] = NA
		data$weight[] = signal
	models$ma.crossover.com = bt.run.share(data, commission = 0.10, clean.signal=T)

```

[![](img/1c062317cfe013f8a9aa503941fc7ce4.png "plot1.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot1-small.png)

The transaction costs reduced the total strategy performance from 5.13 to 4.83

The Backtesting library in the [Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/) was designed with an assumption that there is only one price at which securities are traded each day, by default I used Close prices. The Execution.Price field allows to override this default functionality. In the following example, I modified the 50 / 200 day moving average cross over strategy to Enter trades at the open the next day after the signal.

```

	#*****************************************************************
	# MA cross-over strategy:
	# Exit trades at the close on the day of the signal
	# Enter trades at the open the next day after the signal	
	#****************************************************************** 
	popen = bt.apply(data, Op)		
	signal.new = signal
		trade.start	 = which(signal != mlag(signal) & signal != 0)
		signal.new[trade.start] = 0
		trade.start = trade.start + 1

	data$weight[] = NA
		data$execution.price[] = NA
		data$execution.price[trade.start,] = popen[trade.start,]
		data$weight[] = signal.new
	models$ma.crossover.enter.next.open = bt.run.share(data, clean.signal=T, trade.summary = TRUE)			

	#*****************************************************************
	# Create Report
	#****************************************************************** 	
	# Plot perfromance
	plotbt(models, plotX = T, log = 'y', LeftMargin = 3)	    	
		mtext('Cumulative Performance', side = 2, line = 1)

	# Plot trades
	plotbt.custom.report.part3(models$ma.crossover, trade.summary = TRUE)		
	plotbt.custom.report.part3(models$ma.crossover.enter.next.open, trade.summary = TRUE)		

```

This modification reduced the total strategy performance from 5.13 to 5.09 and we can double check the logic by comparing trades for each strategy below:

[![](img/1cecccea4c84695d63e18601296da7c7.png "plot2.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot2-small.png)

[![](img/933941ef619cd05f98729b966e32488c.png "plot3.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot3-small.png)

To view the complete source code for this example, please have a look at the [bt.execution.price.test() function in bt.test.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r).