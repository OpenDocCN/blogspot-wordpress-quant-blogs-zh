<!--yml

category: 未分类

date: 2024-05-18 14:38:14

-->

# 自适应资产配置 – 敏感性分析 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/08/21/adaptive-asset-allocation-sensitivity-analysis/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/08/21/adaptive-asset-allocation-sensitivity-analysis/#0001-01-01)

今天我想继续讨论[自适应资产配置](http://www.macquarieprivatewealth.ca/dafiles/Internet/mgl/ca/en/advice/specialist/darwin/documents/darwin-adaptive-asset-allocation.pdf)主题，并检查策略结果对用于动量和波动率计算的回溯参数的敏感性。我将按照大卫·瓦拉迪在[自适应资产配置算法参数的鲁棒性](http://cssanalytics.wordpress.com/2012/07/17/adaptive-asset-allocation-combining-momentum-with-minimum-variance/)帖子中概述的示例步骤进行。请参阅我之前的[帖子](https://systematicinvestor.wordpress.com/2012/08/14/adaptive-asset-allocation/)获取更多信息。

让我们首先使用[Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)加载 10 个 ETF 的历史价格：

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

	tickers = spl('SPY,EFA,EWJ,EEM,IYR,RWX,IEF,TLT,DBC,GLD')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)							
	bt.prep(data, align='keep.all', dates='2004:12::')

    #*****************************************************************
    # Code Strategies
    #******************************************************************
    prices = data$prices  
    n = ncol(prices)

    models = list()

    # find period ends
    period.ends = endpoints(prices, 'months')
        period.ends = period.ends[period.ends > 0]

```

接下来，我将 Combo（动量和波动率加权）策略和自适应资产配置（AAA）策略分别封装到 bt.aaa.combo 和 bt.aaa.minrisk 函数中。以下是您如何使用它们的示例：

```

	#*****************************************************************
	# Test
	#****************************************************************** 
	models = list()

	models$combo = bt.aaa.combo(data, period.ends, n.top = 5,
					n.mom = 180, n.vol = 20)

	models$aaa = bt.aaa.minrisk(data, period.ends, n.top = 5,
					n.mom = 180, n.vol = 20)

	plotbt.custom.report.part1(models) 

```

现在让我们使用**Combo**策略评估从 1 到 12 个月的动量和波动率回溯参数的所有可能组合：

```

	#*****************************************************************
	# Sensitivity Analysis: bt.aaa.combo / bt.aaa.minrisk
	#****************************************************************** 
	# length of momentum look back
	mom.lens = ( 1 : 12 ) * 20
	# length of volatility look back
	vol.lens = ( 1 : 12 ) * 20

	models = list()

	# evaluate strategies
	for(n.mom in mom.lens) {
		cat('MOM =', n.mom, '\n')

		for(n.vol in vol.lens) {
			cat('\tVOL =', n.vol, '\n')

			models[[ paste('M', n.mom, 'V', n.vol) ]] = 
				bt.aaa.combo(data, period.ends, n.top = 5,
					n.mom = n.mom, n.vol = n.vol)
		}
	}

	out = plotbt.strategy.sidebyside(models, return.table=T, make.plot = F)

```

最后让我们为每个策略绘制夏普比率、复合年均增长率（Cagr）、动态风险调整指数（DVR）、最大回撤等统计数据：

```

	#*****************************************************************
	# Create Report
	#****************************************************************** 
	# allocate matrix to store backtest results
	dummy = matrix('', len(vol.lens), len(mom.lens))
		colnames(dummy) = paste('M', mom.lens)
		rownames(dummy) = paste('V', vol.lens)

	names = spl('Sharpe,Cagr,DVR,MaxDD')

	layout(matrix(1:4,nrow=2))	
	for(i in names) {
		dummy[] = ''

		for(n.mom in mom.lens)
			for(n.vol in vol.lens)
				dummy[paste('V', n.vol), paste('M', n.mom)] =
					out[i, paste('M', n.mom, 'V', n.vol) ]

		plot.table(dummy, smain = i, highlight = T, colorbar = F)

	}

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/08/plot1-small2.png)

我还为 AAA 策略（bt.aaa.minrisk 函数）重复了最后两个步骤：

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/08/plot2-small2.png)

AAA 和 Combo 策略的结果非常相似。较短期的动量和较短期的波动率产生了最佳结果，但可能以较高的换手成本为代价。

要查看此示例的完整源代码，请查看[github 上的 bt.aaa.sensitivity.test()函数在 bt.test.r 中的代码](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
