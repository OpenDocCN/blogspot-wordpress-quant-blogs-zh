<!--yml

类别：未分类

日期：2024-05-18 14:33:26

-->

# 群集风险平价回测 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2013/03/05/cluster-risk-parity-back-test/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/03/05/cluster-risk-parity-back-test/#0001-01-01)

在[群集投资组合分配](https://systematicinvestor.wordpress.com/2013/02/12/cluster-portfolio-allocation/)一文中，我概述了构建群集风险平价投资组合的 3 个步骤。在每个再平衡期间：

+   创建群集

+   使用风险平价（Risk Parity）在每个群集内分配资金

+   使用风险平价在所有群集之间分配资金

我创建了一个辅助函数，[在 GitHub 上的 strategy.r 中的 distribute.weights() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/strategy.r)，以自动执行这些步骤。它有 2 个参数：

+   分配资金的函数。例如，risk.parity.portfolio，将使用风险平价在和群集之间分配资金。

+   创建群集的函数。例如，cluster.group.kmeans.90，将使用 k-means 算法创建群集

这是将所有内容放在一起的示例。首先，让我们加载 10 个主要资产类别的历史价格：

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
	# Load historical data for ETFs
	#****************************************************************** 
	load.packages('quantmod')

	tickers = spl('GLD,UUP,SPY,QQQ,IWM,EEM,EFA,IYR,USO,TLT')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1900-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)

	bt.prep(data, align='remove.na')

```

接下来，让我们运行 2 个版本的[群集投资组合分配](https://systematicinvestor.wordpress.com/2013/02/12/cluster-portfolio-allocation/)，使用等权重和风险平价算法来分配资金：

```

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 	
	periodicity = 'months'
	lookback.len = 250
	cluster.group = cluster.group.kmeans.90

	obj = portfolio.allocation.helper(data$prices, 
		periodicity = periodicity, lookback.len = lookback.len,
		min.risk.fns = list(
				EW=equal.weight.portfolio,
				RP=risk.parity.portfolio,

				C.EW = distribute.weights(equal.weight.portfolio, cluster.group),
				C.RP=distribute.weights(risk.parity.portfolio, cluster.group)
			)
	) 		

	models = create.strategies(obj, data)$models

```

最后，让我们来检查结果：

```

	#*****************************************************************
	# Create Report
	#****************************************************************** 	
	strategy.performance.snapshoot(models, T)

```

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/03/plot1-small.png)

[群集投资组合分配](https://systematicinvestor.wordpress.com/2013/02/12/cluster-portfolio-allocation/)产生了具有更好的风险调整收益和较小回撤的投资组合。

要查看此示例的完整源代码，请查看 GitHub 上的 bt.test.r 中的 [bt.cluster.portfolio.allocation.test1() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
