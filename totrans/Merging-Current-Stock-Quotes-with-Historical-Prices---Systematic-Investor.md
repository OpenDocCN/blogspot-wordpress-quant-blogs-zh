<!--yml
category: 未分类
date: 2024-05-18 14:38:04
-->

# Merging Current Stock Quotes with Historical Prices | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2012/09/05/merging-current-stock-quotes-with-historical-prices/#0001-01-01](https://systematicinvestor.wordpress.com/2012/09/05/merging-current-stock-quotes-with-historical-prices/#0001-01-01)

I got a question last week about going from the backtest to the trading. For example, if our system is based on today’s close, we can approximate the close value by the price at say 3:30pm, determine the signal and still have time enter the trade. It is not perfect, but one of possible solutions.

Unfortunately calling the getSymbols() function during the trading session will only return closing prices for the prior session. Following is an example I run today during the trading session:

```
	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')

	tickers = spl('VTI,EFA,SHY')	

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)							
	bt.prep(data)

	# look at the data
	last(data$prices, 2)

```

```
> last(data$prices, 2)
             EFA   SHY   VTI
2012-08-30 51.15 84.46 71.78
2012-08-31 51.60 84.51 72.21

```

There is no information for September 4th.

To incorporate current stock quotes, we need to combine current quotes from getQuote() function with historical prices from getSymbols() function. Following is an example I run today during the trading session:

```
	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')

	tickers = spl('VTI,EFA,SHY')	

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)							

		# current quotes logic
		quotes = getQuote(tickers)
		for(i in ls(data))
			if( last(index(data[[i]])) < as.Date(quotes[i, 'Trade Time']) ) {
				data[[i]] = rbind( data[[i]], make.xts(quotes[i, spl('Open,High,Low,Last,Volume,Last')],
					as.Date(quotes[i, 'Trade Time'])))
			}

	bt.prep(data)

	# look at the data
	last(data$prices, 2)

```

```
> last(data$prices, 2)
               EFA    SHY   VTI
2012-08-31 51.6000 84.510 72.21
2012-09-04 51.2561 84.495 71.87

```

The current stock quotes are now present. We can run our strategy at say around 3:30pm, determine the signal and still have time enter the trade.

To view the complete source code for this example, please have a look at the [bt.current.quote.test() function in bt.test.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r).