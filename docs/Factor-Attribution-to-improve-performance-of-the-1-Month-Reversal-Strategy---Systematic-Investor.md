<!--yml

类别：未分类

日期：2024-05-18 14:39:26

-->

# 利用因子归因提高 1 个月反转策略的表现 | 系统性投资者

> 来源：[`systematicinvestor.wordpress.com/2012/07/17/factor-attribution-to-improve-performance-of-the-1-month-reversal-strategy/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/07/17/factor-attribution-to-improve-performance-of-the-1-month-reversal-strategy/#0001-01-01)

今天我想展示如何利用[因子归因](https://systematicinvestor.wordpress.com/2012/07/04/example-of-factor-attribution/)来提升[1 个月反转策略](https://systematicinvestor.wordpress.com/2012/07/13/1-month-reversal-strategy/)的表现。[Blitz, J. Huij, S. Lansdorp, M. Verbeek (2011)的短期残差反转](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1911449)论文提出了这一概念，并讨论了自 1929 年以来应用于美国股市的结果。为了改进 1 个月反转策略的表现，作者们研究了一种基于滚动因子归因回归残差的替代持仓排名指标。

基础的 1 个月反转策略每月通过从 S&P 500 指数中购买 20%的输家并卖空 20%的赢家来形成投资组合，其依据是前一个月的回报率。1 个月**残差**反转策略每月通过从 S&P 500 指数中购买 20%的输家并卖空 20%的赢家来形成投资组合，其依据是滚动因子归因回归的残差。以下是每月形成 1 个月**残差**反转策略投资组合的步骤：

+   1.对 S&P 500 指数中的每家公司，运行前 36 个月的滚动因子归因回归，并计算残差：e.1、e.2、…、e.t、…、e.T，其中 t 在 1:36 之间

+   2.替代持仓排名指标 = e.T / (e 的标准差)

+   3.根据替代持仓排名指标从 S&P 500 指数中购买 20%的输家并卖空 20%的赢家，形成投资组合

让我们首先加载 S&P 500 中所有公司的历史价格，并使用[系统性投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)创建 SPY 和等权重基准：

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

接下来让我们对 S&P 500 指数中的每支股票运行因子归因，以确定其替代持仓排名指标。我将保存 e.T 和 e.T / (e 的标准差)两个指标。

```

# function to compute additional custom stats for factor.rolling.regression
factor.rolling.regression.custom.stats <- function(x,y,fit) {
	n = len(y)
	e = y - x %*% fit$coefficients
	se = sd(e)
	return(c(e[n], e[n]/se))
}

	#*****************************************************************
	# Load factors and align them with prices
	#****************************************************************** 	
	# load Fama/French factors
	factors = get.fama.french.data('F-F_Research_Data_Factors', periodicity = periodicity,download = T, clean = F)

	# align monthly dates
	map = match(format(index(factors$data), '%Y%m'), format(index(prices), '%Y%m'))
		dates = index(factors$data)
		dates[!is.na(map)] = index(prices)[na.omit(map)]
	index(factors$data) = as.Date(dates)

	# add factors and align
	data.fa <- new.env()
		for(i in tickers) data.fa[[i]] = data[[i]][period.ends, ]
		data.fa$factors = factors$data / 100
	bt.prep(data.fa, align='remove.na')

	index = match( index(data.fa$prices), index(data$prices) )
		prices = data$prices[index, ]

	#*****************************************************************
	# Compute Factor Attribution for each ticker
	#****************************************************************** 	

	temp = NA * prices
	factors	= list()
		factors$last.e = temp
		factors$last.e_s = temp

	for(i in tickers) {
		cat(i, '\n')

		# Facto Loadings Regression
		obj = factor.rolling.regression(data.fa, i, 36, silent=T,
			factor.rolling.regression.custom.stats)

		for(j in 1:len(factors))		
			factors[[j]][,i] = obj$fl$custom[,j]

	}

	# add base strategy
	factors$one.month = coredata(prices / mlag(prices))

```

接下来让我们根据 1 个月反转因子将股票分组，并创建报告。

```

	#*****************************************************************
	# Create Quantiles
	#****************************************************************** 
	quantiles = list()

	for(name in names(factors)) {
		cat(name, '\n')
		quantiles[[name]] = bt.make.quintiles(factors[[name]], data, index, start.t =  1+36, prefix=paste(name,'_',sep=''))
	}	

	#*****************************************************************
	# Create Report
	#****************************************************************** 					
	plotbt.custom.report.part1(quantiles$one.month$spread,quantiles$last.e$spread,quantiles$last.e_s$spread)

	plotbt.strategy.sidebyside(quantiles$one.month$spread,quantiles$last.e$spread,quantiles$last.e_s$spread)

	plotbt.custom.report.part1(quantiles$last.e_s)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/07/plot1-small2.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/07/plot2-small2.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/07/plot4-small.png)

过去 10 年来，1 个月**残差**反转策略表现良好，并且大幅优于基础的 1 个月反转策略。

要查看此示例的完整源代码，请查看 [GitHub 上 bt.test.r 中的 bt.fa.one.month.test() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
