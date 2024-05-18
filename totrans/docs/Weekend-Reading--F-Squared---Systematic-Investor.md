<!--yml
category: 未分类
date: 2024-05-18 14:31:04
-->

# Weekend Reading: F-Squared | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2013/12/07/weekend-reading-f-squared/#0001-01-01](https://systematicinvestor.wordpress.com/2013/12/07/weekend-reading-f-squared/#0001-01-01)

Mebane Faber posted another interesting blog post: [Building a Simple Sector Rotation on Momentum and Trend](http://www.mebanefaber.com/2013/12/04/square-root-of-f-squared/) that caught my interest. Today I want to show how you can test such strategy using the [Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/):

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

	data = new.env()
	# load historical market returns
	temp = get.fama.french.data('F-F_Research_Data_Factors', periodicity = '',download = T, clean = T)
		ret = cbind(temp[[1]]$Mkt.RF + temp[[1]]$RF, temp[[1]]$RF)
		price = bt.apply.matrix(ret / 100, function(x) cumprod(1 + x))
	data$SPY = make.stock.xts( price$Mkt.RF )
	data$SHY = make.stock.xts( price$RF )

	# load historical sector returns
	temp = get.fama.french.data('10_Industry_Portfolios', periodicity = '',download = T, clean = T)		
		ret = temp[[1]]
		price = bt.apply.matrix(ret[,1:9] / 100, function(x) cumprod(1 + x))
	for(n in names(price)) data[[n]] = make.stock.xts( price[,n] )

	# align dates
	data$symbolnames = c(names(price), 'SHY', 'SPY')
	bt.prep(data, align='remove.na', dates='2000::')

	# back-test dates
	bt.dates = '2001:04::'

	#*****************************************************************
	# Setup
	#****************************************************************** 	
	prices = data$prices  
	n = ncol(data$prices)

	models = list()

	#*****************************************************************
	# Benchmark Strategies
	#****************************************************************** 			
	data$weight[] = NA
		data$weight$SPY[1] = 1
	models$SPY = bt.run.share(data, clean.signal=F, dates=bt.dates)

	weight = prices
		weight$SPY = NA
		weight$SHY = NA

	data$weight[] = NA
		data$weight[] = ntop(weight[], n)
	models$EW = bt.run.share(data, clean.signal=F, dates=bt.dates)

	#*****************************************************************
	# Code Strategies
	# http://www.mebanefaber.com/2013/12/04/square-root-of-f-squared/
	#****************************************************************** 			
	sma = bt.apply.matrix(prices, SMA, 10)

	# create position score
	position.score = sma
	position.score[ prices < sma ] = NA
		position.score$SHY = NA	
		position.score$SPY = NA	

	# equal weight allocation
	weight = ntop(position.score[], n)	

	# number of invested funds
	n.selected = rowSums(weight != 0)

	# cash logic
	weight$SHY[n.selected == 0,] = 1

	weight[n.selected == 1,] = 0.25 * weight[n.selected == 1,]
	weight$SHY[n.selected == 1,] = 0.75

	weight[n.selected == 2,] = 0.5 * weight[n.selected == 2,]
	weight$SHY[n.selected == 2,] = 0.5

	weight[n.selected == 3,] = 0.75 * weight[n.selected == 3,]
	weight$SHY[n.selected == 3,] = 0.25

	# cbind(round(100*weight,0), n.selected)	

	data$weight[] = NA
		data$weight[] = weight
	models$strategy1 = bt.run.share(data, clean.signal=F, dates=bt.dates)	

	#*****************************************************************
	# Create Report
	#******************************************************************       	
	strategy.performance.snapshoot(models, one.page = T)

```

[![plot1](img/c5577ae3783461b37f5a035fbc1c0808.png)](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/12/plot11.png)

Mebane thank you very much for sharing your great ideas. I would encourage readers to play with this strategy and report back.

Please note that I back-tested the strategy using the monthly observations. The strategy’s draw-down is around 17% using monthly data. If we switch to the daily data, the strategy’s draw-down goes to around 22%. There was one really bad month in 2002.

To view the complete source code for this example, please have a look at the [bt.mebanefaber.f.squared.test() function in bt.test.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r).