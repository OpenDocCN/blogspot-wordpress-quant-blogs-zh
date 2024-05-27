<!--yml

类别：未分类

日期：2024-05-18 14:37:39

-->

# 最小相关算法示例 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/09/24/minimum-correlation-algorithm-example/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/09/24/minimum-correlation-algorithm-example/#0001-01-01)

今日我想对[最小相关算法论文](https://systematicinvestor.wordpress.com/2012/09/22/minimum-correlation-algorithm-paper/)进行跟进，并展示如何将最小相关算法纳入您的投资组合构建工作流程，并解释为什么我喜欢最小相关算法。

首先，让我们加载用于[最小相关算法论文](https://systematicinvestor.wordpress.com/2012/09/22/minimum-correlation-algorithm-paper/)的 ETF 数据集，使用[系统投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)。

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
	load.packages('quantmod,quadprog')
	tickers = spl('SPY,QQQ,EEM,IWM,EFA,TLT,IYR,GLD')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)							
	bt.prep(data, align='keep.all', dates='2002:08::')

```

接下来，我创建了 portfolio.allocation.helper()函数，以简化投资组合构建算法的回测：

```

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 	

	obj = portfolio.allocation.helper(data$prices, periodicity = 'weeks',
		min.risk.fns = list(EW=equal.weight.portfolio,
						RP=risk.parity.portfolio,
						MV=min.var.portfolio,
						MD=max.div.portfolio,
						MC=min.corr.portfolio,
						MC2=min.corr2.portfolio),
		custom.stats.fn = 'portfolio.allocation.custom.stats'
	) 

	models = create.strategies(obj, data)$models

```

请注意，我在上面的代码中为各种投资组合分配算法分配了缩写。

例如，最小相关算法的缩写是 MC，实际进行所有计算的功能是 min.corr.portfolio()函数。

接下来，让我们创建各种摘要报告以查看不同算法的表现和分配：

```

    #*****************************************************************
    # Create Report
    #******************************************************************       
	# Plot perfromance
	layout(1:2)
	plotbt(models, plotX = T, log = 'y', LeftMargin = 3)	    	
		mtext('Cumulative Performance', side = 2, line = 1)

	out = plotbt.strategy.sidebyside(models, return.table=T)

	# Plot time series of components of Composite Diversification Indicator
	cdi = custom.composite.diversification.indicator(obj,plot.table = F)	
		out = rbind(colMeans(cdi, na.rm=T), out)
		rownames(out)[1] = 'Composite Diversification Indicator(CDI)'

	# Portfolio Turnover for each strategy
	y = 100 * sapply(models, compute.turnover, data)
		out = rbind(y, out)
		rownames(out)[1] = 'Portfolio Turnover'		

	# Plot and compare strategies across different metrics
	performance.barchart.helper(out, 'Sharpe,Cagr,DVR,MaxDD', c(T,T,T,T))

	performance.barchart.helper(out, 'Volatility,Portfolio Turnover,Composite Diversification Indicator(CDI)', c(F,F,T))

	# Plot transition maps
	layout(1:len(models))
	for(m in names(models)) {
		plotbt.transition.map(models[[m]]$weight, name=m)
			legend('topright', legend = m, bty = 'n')
	}

	# Plot transition maps for Risk Contributions
	dates = index(data$prices)[obj$period.ends]
	for(m in names(models)) {
		plotbt.transition.map(make.xts(obj$risk.contributions[[m]], dates), 
		name=paste('Risk Contributions',m))
			legend('topright', legend = m, bty = 'n')
	}

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/09/plot1-small2.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/09/plot2-small1.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/09/plot3-small2.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/09/plot4-small1.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/09/plot5-small.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/09/plot6-small.png)

查看摘要统计数据，您可能会想知道最小相关算法有何不同，以及为什么我喜欢它？

最小相关算法的整体特性使其对我具有吸引力。特别是，它的性能合理，回撤有限，换手率低，复合多样化得分高。这些吸引人的特性的结合确实将最小相关算法与其他算法区分开来。

在下一篇文章中，我将展示最小相关算法的速度基准。

要查看此例的完整源代码，请查看[github 上的 bt.mca.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
