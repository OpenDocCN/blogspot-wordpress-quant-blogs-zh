<!--yml

类别：未分类

日期：2024-05-18 14:40:23

-->

# 波动率分位数 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/06/05/volatility-quantiles/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/06/05/volatility-quantiles/#0001-01-01)

今天我想要检验标普 500 指数中股票的表现，将其分组为[分位数](http://en.wikipedia.org/wiki/Quantile)，基于一年的历史波动率。这个想法非常简单：每周我们将根据一年的历史波动率将标普 500 指数中的股票分组为波动率分位数投资组合。接下来我们将对每个投资组合进行回测，并检查低历史波动率是否对应低实现波动率。

让我们首先加载标普 500 指数中所有公司的历史价格，并使用[Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)创建 SPY 和 Equal Weight benchmarks：

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
	tickers = sp500.components()$tickers

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)
		# remove companies with less than 5 years of data
		rm.index = which( sapply(ls(data), function(x) nrow(data[[x]])) < 1000 )	
		rm(list=names(rm.index), envir=data)

		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)		
	bt.prep(data, align='keep.all', dates='1994::')

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
		data$weight[] = ntop(prices, 500)
	models$equal.weight = bt.run(data)	

```

接下来让我们根据一年的历史波动率将标普 500 指数中的股票分成分位数，并为每个分位数创建回测。

```

	#*****************************************************************
	# Create Quantiles based on the historical one year volatility 
	#****************************************************************** 
	# setup re-balancing periods
	period.ends = endpoints(prices, 'weeks')
		period.ends = period.ends[period.ends > 0]

	# compute historical one year volatility
	p = bt.apply.matrix(coredata(prices), ifna.prev)	
	ret = p / mlag(p) - 1		
	sd252 = bt.apply.matrix(ret, runSD, 252)		

	# split stocks in the S&amp;P 500 into Quantiles using one year historical Volatility
	n.quantiles=5
	start.t = which(period.ends >= (252+2))[1]	
	quantiles = weights = p * NA

	for( t in start.t:len(period.ends) ) {
		i = period.ends[t]

		factor = sd252[i,]
		ranking = ceiling(n.quantiles * rank(factor, na.last = 'keep','first') / count(factor))

		quantiles[i,] = ranking
		weights[i,] = 1/tapply(rep(1,n), ranking, sum)[ranking]			
	}

	quantiles = ifna(quantiles,0)

	#*****************************************************************
	# Create backtest for each Quintile
	#****************************************************************** 
	for( i in 1:n.quantiles) {
		temp = weights * NA
		temp[period.ends,] = 0
		temp[quantiles == i] = weights[quantiles == i]

		data$weight[] = NA
			data$weight[] = temp
		models[[ paste('Q',i,sep='_') ]] = bt.run(data, silent = T)
	}

```

最后让我们为每个波动率分位数绘制历史股票曲线并创建一个总结表格。

```

	#*****************************************************************
	# Create Report
	#****************************************************************** 					
	plotbt.custom.report.part1(models)		
	plotbt.strategy.sidebyside(models)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/06/plot1-small.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/06/plot2-small.png)

我们的论点适用于标普 500 指数中的股票：低历史波动率导致低实现波动率。历史波动率分位数与实现波动率分位数一一对应。

请注意，性能数字必须经过一定程度的怀疑，因为我使用了标普 500 指数中的**当前**成分；因此，引入了[存活偏见](http://en.wikipedia.org/wiki/Survivorship_bias)。

要查看此示例的完整源代码，请查看[github 上 bt.test.r 中的 bt.volatility.quantiles.test() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
