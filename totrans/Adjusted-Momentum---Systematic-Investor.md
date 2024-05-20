<!--yml
category: 未分类
date: 2024-05-18 14:29:45
-->

# Adjusted Momentum | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2014/08/01/adjusted-momentum/#0001-01-01](https://systematicinvestor.wordpress.com/2014/08/01/adjusted-momentum/#0001-01-01)

## Adjusted Momentum

David Varadi has published two excellent posts / ideas about cooking with momentum:

I just could not resist the urge to share these ideas with you. Following is implementation using the [Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/).

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

	tickers = spl('SPY,^VIX')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)
		for(i in data$symbolnames) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)
	bt.prep(data, align='remove.na', fill.gaps = T)

	VIX = Cl(data$VIX)
	bt.prep.remove.symbols(data, 'VIX')

	#*****************************************************************
	# Setup
	#*****************************************************************
	prices = data$prices

	models = list()

	#*****************************************************************
	# 200 SMA
	#****************************************************************** 
	data$weight[] = NA
		data$weight[] = iif(prices > SMA(prices, 200), 1, 0)
	models$ma200 = bt.run.share(data, clean.signal=T)

	#*****************************************************************
	# 200 ROC
	#****************************************************************** 
	roc = prices / mlag(prices) - 1

	data$weight[] = NA
		data$weight[] = iif(SMA(roc, 200) > 0, 1, 0)
	models$roc200 = bt.run.share(data, clean.signal=T)

	#*****************************************************************
	# 200 VIX MOM
	#****************************************************************** 
	data$weight[] = NA
		data$weight[] = iif(SMA(roc/VIX, 200) > 0, 1, 0)
	models$vix.mom = bt.run.share(data, clean.signal=T)

	#*****************************************************************
	# 200 ER MOM
	#****************************************************************** 
	forecast = SMA(roc,10)
	error = roc - mlag(forecast)
	mae = SMA(abs(error), 10)

	data$weight[] = NA
		data$weight[] = iif(SMA(roc/mae, 200) > 0, 1, 0)
	models$er.mom = bt.run.share(data, clean.signal=T)

	#*****************************************************************
	# Report
	#****************************************************************** 
	strategy.performance.snapshoot(models, T)

```

[![plot1](img/8c80c5e63788d6aea18f031b858a0be9.png)](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/08/plot1.png)

**Please enjoy and share your ideas with David and myself.**

To view the complete source code for this example, please have a look at the
[bt.adjusted.momentum.test() function in bt.test.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r).