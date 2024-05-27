<!--yml

分类：未分类

日期：2024-05-18 14:39:43

-->

# 因子归因示例 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/07/04/example-of-factor-attribution/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/07/04/example-of-factor-attribution/#0001-01-01)

在之前的帖子中，[因子归因 2](https://systematicinvestor.wordpress.com/2012/06/27/factor-attribution-2/)，我展示了如何将因子归因应用于分解基金的回报，包括市场、资本化和价值因子，法玛和弗伦奇的[“三因子模型”](http://en.wikipedia.org/wiki/Fama%E2%80%93French_three-factor_model)。今天，我想向你展示因子归因的另一个应用。首先，让我们对标准普尔 500 指数中的每支股票运行因子归因，以确定其价值敞口。接下来，让我们根据价值敞口将股票分组到分位数，并为每个分位数创建回测。我将依赖[波动率分位数](https://systematicinvestor.wordpress.com/2012/06/05/volatility-quantiles/)帖子中的代码来创建分位数。

让我们首先加载标准普尔 500 指数当前所有成分股的历史价格。

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
	tickers = sp500.components()$tickers

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)
		# remove companies with less than 5 years of data
		rm.index = which( sapply(ls(data), function(x) nrow(data[[x]])) < 1000 )	
		rm(list=names(rm.index), envir=data)

		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)		
	bt.prep(data, align='keep.all', dates='1994::')
		tickers = data$symbolnames

	data.spy <- new.env()
	getSymbols('SPY', src = 'yahoo', from = '1970-01-01', env = data.spy, auto.assign = T)
	bt.prep(data.spy, align='keep.all', dates='1994::')

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 
	prices = data$prices
		nperiods = nrow(prices)
		n = ncol(prices)

	models = list()

	# SPY
	data.spy$weight[] = NA
		data.spy$weight[] = 1
	models$spy = bt.run(data.spy)

	# Equal Weight
	data$weight[] = NA
		data$weight[] = ntop(prices, n)
	models$equal.weight = bt.run(data)

```

接下来让我们对标准普尔 500 指数中的每支股票运行因子归因，以确定其价值敞口。

```

	#*****************************************************************
	# Compute Factor Attribution for each ticker
	#****************************************************************** 
	periodicity = 'weeks'

	# load Fama/French factors
	factors = get.fama.french.data('F-F_Research_Data_Factors', periodicity = periodicity,download = T, clean = F)

	period.ends = endpoints(data$prices, periodicity)
		period.ends = period.ends[period.ends > 0]

	# add factors and align
	data.fa <- new.env()
		for(i in tickers) data.fa[[i]] = data[[i]][period.ends,]
	data.fa$factors = factors$data / 100
	bt.prep(data.fa, align='remove.na')

	index = match( index(data.fa$prices), index(data$prices) )
	measure = data$prices[ index, ]	
	for(i in tickers) {
		cat(i, '\n')

		# Facto Loadings Regression
		obj = factor.rolling.regression(data.fa, i, 36, silent=T)

		measure[,i] = coredata(obj$fl$estimate$HML)
	}

```

最后，让我们根据价值敞口将股票分组到分位数，并为每个分位数创建回测。

```

	#*****************************************************************
	# Create Value Quantiles
	#****************************************************************** 
	n.quantiles=5
	start.t = 1+36
	quantiles = weights = coredata(measure) * NA			

	for( t in start.t:nrow(weights) ) {
		factor = as.vector(coredata(measure[t,]))
		ranking = ceiling(n.quantiles * rank(factor, na.last = 'keep','first') / count(factor))

		quantiles[t,] = ranking
		weights[t,] = 1/tapply(rep(1,n), ranking, sum)[ranking]			
	}

	quantiles = ifna(quantiles,0)

	#*****************************************************************
	# Create backtest for each Quintile
	#****************************************************************** 
	for( i in 1:n.quantiles) {
		temp = weights * NA
			temp[] = 0
		temp[quantiles == i] = weights[quantiles == i]

		data$weight[] = NA
			data$weight[index,] = temp
		models[[ paste('Q',i,sep='_') ]] = bt.run(data, silent = T)
	}

	#*****************************************************************
	# Create Report
	#****************************************************************** 					
	plotbt.custom.report.part1(models)		

	plotbt.strategy.sidebyside(models)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/07/plot1-small.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/07/plot2-small.png)

Value Quantiles 与历史表现之间没有线性关系。我也怀疑暗示的价值敞口可能与每支股票的真实价格/账面价值比相差很大。请告诉我你对这种方法的看法。

在下一篇帖子中，我将展示因子归因的另一个示例。

要查看此示例的完整源代码，请查看[Github 上的 bt.fa.value.quantiles.test() 函数的 bt.test.r](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
