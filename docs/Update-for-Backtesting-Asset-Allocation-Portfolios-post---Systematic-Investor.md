<!--yml

类别：未分类

日期：2024-05-18 14:29:32

-->

# 更新回测资产配置组合文章 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2013/10/24/update-for-backtesting-asset-allocation-portfolios-post/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/10/24/update-for-backtesting-asset-allocation-portfolios-post/#0001-01-01)

自从我最初的帖子[回测资产配置组合](https://systematicinvestor.wordpress.com/2012/03/19/backtesting-asset-allocation-portfolios/)发表以来已经过去了一年多。在这段时间里，我扩展了[系统投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)的功能，包括优化函数和辅助回测函数。

今天，我想更新[回测资产配置组合](https://systematicinvestor.wordpress.com/2012/03/19/backtesting-asset-allocation-portfolios/)的文章并展示新功能。我将使用以下全球资产组合：SPY, QQQ, EEM, IWM, EFA, TLT, IYR, GLD，每月使用不同的资产配置方法来形成组合。

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
	load.packages('quantmod,quadprog,corpcor,lpSolve')
	tickers = spl('SPY,QQQ,EEM,IWM,EFA,TLT,IYR,GLD')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)							
	bt.prep(data, align='remove.na', dates='1990::') 

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 					
	cluster.group = cluster.group.kmeans.90

	obj = portfolio.allocation.helper(data$prices, 
		periodicity = 'months', lookback.len = 60, 
		min.risk.fns = list(
			EW=equal.weight.portfolio,
			RP=risk.parity.portfolio(),
			MD=max.div.portfolio,						

			MV=min.var.portfolio,
			MVE=min.var.excel.portfolio,
			MV2=min.var2.portfolio,

			MC=min.corr.portfolio,
			MCE=min.corr.excel.portfolio,
			MC2=min.corr2.portfolio,

			MS=max.sharpe.portfolio(),
			ERC = equal.risk.contribution.portfolio,

			# target retunr / risk
			TRET.12 = target.return.portfolio(12/100),								
			TRISK.10 = target.risk.portfolio(10/100),

			# cluster
			C.EW = distribute.weights(equal.weight.portfolio, cluster.group),
			C.RP = distribute.weights(risk.parity.portfolio, cluster.group),

			# rso
			RSO.RP.5 = rso.portfolio(risk.parity.portfolio, 5, 500), 

			# others
			MMaxLoss = min.maxloss.portfolio,
			MMad = min.mad.portfolio,
			MCVaR = min.cvar.portfolio,
			MCDaR = min.cdar.portfolio,
			MMadDown = min.mad.downside.portfolio,
			MRiskDown = min.risk.downside.portfolio,
			MCorCov = min.cor.insteadof.cov.portfolio
		)
	)

	models = create.strategies(obj, data)$models

	#*****************************************************************
	# Create Report
	#******************************************************************    
	strategy.performance.snapshoot(models, T, 'Backtesting Asset Allocation portfolios')

```

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/10/plot1.png)

我希望你能享受创建自己的资产组合配置方法，或者尝试大量现成的、可供你实验的资产组合配置技术。

要查看此示例的完整源代码，请参阅 github 上的 [bt.aa.test.new() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
