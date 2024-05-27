<!--yml

分类：未分类

日期：2024-05-18 14:39:35

-->

# 1-Month Reversal Strategy | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/07/13/1-month-reversal-strategy/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/07/13/1-month-reversal-strategy/#0001-01-01)

今日我想展示一个 1-Month Reversal Strategy 的简单示例。每月我们将购买 S&P 500 指数中 20%的输家并做空 20%的赢家。输赢依据前一个月的回报率衡量。本文将为此后一篇关于因子归因如何提升 1-Month Reversal Strategy 表现的帖子奠定基础。以下是下一篇文章的参考资料，若您想预先了解，请参阅[D. Blitz, J. Huij, S. Lansdorp, M. Verbeek (2011)的《Short-Term Residual Reversal》](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1911449)论文。

首先，加载 S&P 500 所有公司的历史价格，并使用[Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)创建 SPY 和等权重基准：

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
		n = ncol(prices)

	#*****************************************************************
	# Setup monthly periods
	#****************************************************************** 
	periodicity = 'months'

	period.ends = endpoints(data$prices, periodicity)
		period.ends = period.ends[period.ends > 0]

	prices = prices[period.ends, ]		

	#*****************************************************************
	# Create Benchmarks, omit results for the first 36 months - to be consistent with Factor Attribution
	#****************************************************************** 	
	models = list()

	# SPY
	data.spy$weight[] = NA
		data.spy$weight[] = 1
		data.spy$weight[1:period.ends[36],] = NA
	models$spy = bt.run(data.spy)

	# Equal Weight
	data$weight[] = NA
		data$weight[period.ends,] = ntop(prices, n)
		data$weight[1:period.ends[36],] = NA		
	models$equal.weight = bt.run(data)

```

接下来，根据 1 个月回报将股票分组至各分位数，并为每个分位数创建回测。我将依赖[《Volatility Quantiles》](https://systematicinvestor.wordpress.com/2012/06/05/volatility-quantiles/)一文中的代码来创建分位数。

```

	#*****************************************************************
	# Create Reversal Quantiles
	#****************************************************************** 
	n.quantiles = 5
	start.t = 1 + 36
	quantiles = weights = coredata(prices) * NA			

	one.month = coredata(prices / mlag(prices))

	for( t in start.t:nrow(weights) ) {
		factor = as.vector(one.month[t,])
		ranking = ceiling(n.quantiles * rank(factor, na.last = 'keep','first') / count(factor))

		quantiles[t,] = ranking
		weights[t,] = 1/tapply(rep(1,n), ranking, sum)[ranking]			
	}

	quantiles = ifna(quantiles,0)

	#*****************************************************************
	# Create backtest for each Quintile
	#****************************************************************** 
	temp = weights * NA

	for( i in 1:n.quantiles) {
		temp[] = 0
		temp[quantiles == i] = weights[quantiles == i]

		data$weight[] = NA
			data$weight[period.ends,] = temp
		models[[ paste('M1_Q',i,sep='') ]] = bt.run(data, silent = T)
	}

```

最后，我们将构建 Q1/Q5 价差并生成综合绩效报告。

```

	#*****************************************************************
	# Create Q1-Q5 spread
	#****************************************************************** 
	temp[] = 0
	temp[quantiles == 1] = weights[quantiles == 1]
	temp[quantiles == n.quantiles] = -weights[quantiles == n.quantiles]

	data$weight[] = NA
		data$weight[period.ends,] = temp
	models$spread = bt.run(data, silent = T)	

	#*****************************************************************
	# Create Report
	#****************************************************************** 	
	plotbt.custom.report.part1(models)

	plotbt.custom.report.part1(models[spl('spy,equal.weight,spread')])

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/07/plot1-small1.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/07/plot2-small1.png)

在下一篇文章中，我将展示如何利用[D. Blitz, J. Huij, S. Lansdorp, M. Verbeek (2011)的《Short-Term Residual Reversal》](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1911449)论文中提出的方法论，通过因子归因提升 1-Month Reversal Strategy 的表现。

如需查看此示例的完整源代码，请参阅[GitHub 上 bt.test.r 文件中的 bt.one.month.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
