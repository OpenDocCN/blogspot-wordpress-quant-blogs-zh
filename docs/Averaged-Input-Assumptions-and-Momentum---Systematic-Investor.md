<!--yml

category: 未分类

date: 2024-05-18 14:31:12

-->

# 平均输入假设和动量 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2013/12/05/averaged-input-assumptions-and-momentum/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/12/05/averaged-input-assumptions-and-momentum/#0001-01-01)

今天我想分享由 Pierre Chretien 贡献的另一个有趣的想法。 Pierre 建议使用**平均**输入假设和动量来创建一个**相对安静**的策略。 **平均**技术用于避免过度拟合任何特定频率。

为了创建**平均**输入假设，我们结合不同回看期间的收益，给予最近的收益更多的权重，形成整体输入假设。

```

create.ia.averaged <- function(lookbacks, n.lag) {
	lookbacks = lookbacks
	n.lag = n.lag

	function(hist.returns, index=1:ncol(hist.returns), hist.all)
	{	
		nperiods = nrow(hist.returns)

		temp = c()
		for (n.lookback in lookbacks) 
			temp = rbind(temp, hist.returns[(nperiods - n.lookback - n.lag + 1):(nperiods - n.lag), ])
		create.ia(temp, index, hist.all)
	}	
}

```

要创建**平均**动量，我们查看加权平均动量，该动量是在不同回看期间计算得出的。

```

momentum.averaged <- function(prices, 
	lookbacks = c(20,60,120,250) ,	# length of momentum look back
	n.lag = 3
) {
	momentum = 0 * prices
	for (n.lookback in lookbacks) {
		part.mom = mlag(prices, n.lag) / mlag(prices, n.lookback + n.lag) - 1
		momentum = momentum + 252 / n.lookback * part.mom
	}
	momentum / len(lookbacks)
}

```

接下来，让我们比较使用历史输入假设与**平均**输入假设以及动量与**平均**动量。 我将考虑绝对动量（而不是横截面），有关相对动量和绝对动量的更多信息，请参见

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

	# 10 funds
	tickers = spl('Us.Eq = VTI + VTSMX,
	Eurpoe.Eq = IEV + FIEUX,
	Japan.Eq = EWJ + FJPNX,
	Emer.Eq = EEM + VEIEX,
	Re = RWX + VNQ + VGSIX,		
	Com = DBC + QRAAX,
	Gold = GLD + SCGDX,
	Long.Tr = TLT + VUSTX,
	Mid.Tr = IEF + VFITX,
	Short.Tr = SHY + VFISX') 

	start.date = 1998

	dates = paste(start.date,'::',sep='') 

	data <- new.env()
	getSymbols.extra(tickers, src = 'yahoo', from = '1980-01-01', env = data, set.symbolnames = T, auto.assign = T)
		for(i in data$symbolnames) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)
	bt.prep(data, align='keep.all', dates=paste(start.date-2,':12::',sep=''), fill.gaps = T)

	#*****************************************************************
	# Setup
	#****************************************************************** 		
	prices = data$prices   
		n = ncol(prices)
		nperiods = nrow(prices)

	periodicity = 'months'
	period.ends = endpoints(prices, periodicity)
		period.ends = period.ends[period.ends > 0]

	max.product.exposure = 0.6	

	#*****************************************************************
	# Input Assumptions
	#****************************************************************** 	
	lookback.len = 40
	create.ia.fn = create.ia

	# input assumptions are averaged on 20, 40, 60 days using 1 day lag
	ia.array = c(20,40,60)
	avg.create.ia.fn = create.ia.averaged(ia.array, 1)

	#*****************************************************************
	# Momentum
	#****************************************************************** 	
	universe = prices > 0

	mom.lookback.len = 120	
	momentum = prices / mlag(prices, mom.lookback.len) - 1
	mom.universe = ifna(momentum > 0, F)

	# momentum is averaged on 20,60,120,250 days using 3 day lag
	mom.array = c(20,60,120,250)	
	avg.momentum = momentum.averaged(prices, mom.array, 3)
	avgmom.universe = ifna(avg.momentum > 0, F)

	#*****************************************************************
	# Algos
	#****************************************************************** 	
	min.risk.fns = list(
		EW = equal.weight.portfolio,
		MV = min.var.portfolio,
		MCE = min.corr.excel.portfolio,

		MV.RSO = rso.portfolio(min.var.portfolio, 3, 100, const.ub = max.product.exposure),
		MCE.RSO = rso.portfolio(min.corr.excel.portfolio, 3, 100, const.ub = max.product.exposure)
	)

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 	
make.strategy.custom <- function(name, create.ia.fn, lookback.len, universe, env) {
	obj = portfolio.allocation.helper(data$prices, 
		periodicity = periodicity,
		universe = universe,
		lookback.len = lookback.len,
		create.ia.fn = create.ia.fn,
		const.ub = max.product.exposure,
		min.risk.fns = min.risk.fns,
		adjust2positive.definite = F
	)
	env[[name]] = create.strategies(obj, data, prefix=paste(name,'.',sep=''))$models
}

	models <- new.env()	
	make.strategy.custom('ia.none'        , create.ia.fn    , lookback.len, universe       , models)
	make.strategy.custom('ia.mom'         , create.ia.fn    , lookback.len, mom.universe   , models)
	make.strategy.custom('ia.avg_mom'     , create.ia.fn    , lookback.len, avgmom.universe, models)
	make.strategy.custom('avg_ia.none'    , avg.create.ia.fn, 252         , universe       , models)
	make.strategy.custom('avg_ia.mom'     , avg.create.ia.fn, 252         , mom.universe   , models)
	make.strategy.custom('avg_ia.avg_mom' , avg.create.ia.fn, 252         , avgmom.universe, models)

	#*****************************************************************
	# Create Report
	#*****************************************************************		
strategy.snapshot.custom <- function(models, n = 0, title = NULL) {
	if (n > 0)
		models = models[ as.vector(matrix(1:len(models),ncol=n, byrow=T)) ]	

	layout(1:3)	
	plotbt(models, plotX = T, log = 'y', LeftMargin = 3, main = title)
		mtext('Cumulative Performance', side = 2, line = 1)
	plotbt.strategy.sidebyside(models)
	barplot.with.labels(sapply(models, compute.turnover, data), 'Average Annual Portfolio Turnover', T)	
}

	# basic vs basic + momentum => momentum filter has better results
	models.final = c(models$ia.none, models$ia.mom)
	strategy.snapshot.custom(models.final, len(min.risk.fns), 'Momentum Filter')

	# basic vs basic + avg ia => averaged ia reduce turnover
	models.final = c(models$ia.none, models$avg_ia.none)
	strategy.snapshot.custom(models.final, len(min.risk.fns), 'Averaged Input Assumptions')

	# basic + momentum vs basic + avg.momentum => mixed results for averaged momentum
	models.final = c(models$ia.mom, models$ia.avg_mom)
	strategy.snapshot.custom(models.final, len(min.risk.fns), 'Averaged Momentum')

	# basic + momentum vs avg ia + avg.momentum
	models.final = c(models$ia.mom, models$avg_ia.avg_mom)
	strategy.snapshot.custom(models.final, len(min.risk.fns), 'Averaged vs Base')	

```

上面，我比较了以下 4 种情况的结果：

1\. 添加动量过滤器：所有算法表现更好

![plot3](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/12/plot3.png)

2\. 输入假设 vs **平均**输入假设：收益非常相似，但使用**平均**输入假设有助于减少投资组合的周转率。

![plot2](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/12/plot2.png)

3\. 动量 vs **平均** 动量：收益非常相似，但使用**平均**动量会增加投资组合的周转率。

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/12/plot1.png)

4\. 历史输入假设 + 动量 vs **平均**输入假设 + **平均**动量：结果参差不齐，使用**平均**方法没有一致的优势

![plot4](img/3ac4e7b8d406f9d820d0ebe211916486.png)

总的来说，**平均**方法是一个非常有趣的想法，我希望你会尝试并分享你的发现，就像 Pierre 一样。 Pierre，再次非常感谢你的分享。

[bt.averaged.test()函数的完整源代码和示例在 github 的 bt.test.r 中可用](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r).
