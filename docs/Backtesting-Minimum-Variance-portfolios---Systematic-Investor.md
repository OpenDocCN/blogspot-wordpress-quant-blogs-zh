<!--yml

分类：未分类

日期：2024-05-18 14:38:43

-->

# 最小方差组合的回测 | 系统化投资者

> 来源：[`systematicinvestor.wordpress.com/2011/12/13/backtesting-minimum-variance-portfolios/#0001-01-01`](https://systematicinvestor.wordpress.com/2011/12/13/backtesting-minimum-variance-portfolios/#0001-01-01)

我想展示如何将我在撰写有关[资产配置](https://systematicinvestor.wordpress.com/category/asset-allocation/)系列文章时讨论的各种风险度量与[系统化投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)中的回测库相结合。我将以最小方差组合作为本文的示例。

我建议阅读 Quantivity 在[最小方差行业轮动](http://quantivity.wordpress.com/2011/04/20/minimum-variance-sector-rotation/)一文中对最小方差组合进行的良好讨论。

我将使用大卫·瓦拉迪在[无需预测的算法：战术策略的新基准](http://cssanalytics.wordpress.com/2011/08/09/forecast-free-algorithms-a-new-benchmark-for-tactical-strategies/)一文中概述的投资范围和调仓计划。投资范围：

| 1\. 标准普尔 500 ([SPY](http://www.google.com/finance?q=SPY)) |
| --- |
| 2\. 纳斯达克 100 ([QQQ](http://www.google.com/finance?q=QQQ)) |
| 3\. 新兴市场 ([EEM](http://www.google.com/finance?q=EEM)) |
| 4\. 罗素 2000 ([IWM](http://www.google.com/finance?q=IWM)) |
| 5\. MSCI 欧洲亚太及非洲地区指数 ([EFA](http://www.google.com/finance?q=EFA)) |
| 6\. 长期国库债券 ([TLT](http://www.google.com/finance?q=TLT)) |
| 7\. 房地产 ([IYR](http://www.google.com/finance?q=IYR)) |
| 8\. 黄金 ([GLD](http://www.google.com/finance?q=GLD)) |

调仓是按周进行的，季度数据用于估计输入假设。

以下代码实现了这一策略，使用的是[系统化投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)中的回测库：

```

# Load Systematic Investor Toolbox (SIT)
setInternet2(TRUE)
con = gzcon(url('https://github.com/systematicinvestor/SIT/raw/master/sit.gz', 'rb'))
	source(con)
close(con)

	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod,quadprog,lpSolve')
	tickers = spl('SPY,QQQ,EEM,IWM,EFA,TLT,IYR,GLD')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)

	data.weekly <- new.env()
		for(i in tickers) data.weekly[[i]] = to.weekly(data[[i]], indexAt='endof')

	bt.prep(data, align='remove.na', dates='1990::2011')
	bt.prep(data.weekly, align='remove.na', dates='1990::2011')

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 
	prices = data$prices   
	n = ncol(prices)

	# find week ends
	week.ends = endpoints(prices, 'weeks')
		week.ends = week.ends[week.ends > 0]		

	# Equal Weight 1/N Benchmark
	data$weight[] = NA
		data$weight[week.ends,] = ntop(prices[week.ends,], n)		

		capital = 100000
		data$weight[] = (capital / prices) * data$weight
	equal.weight = bt.run(data, type='share')

	#*****************************************************************
	# Create Constraints
	#*****************************************************************
	constraints = new.constraints(n, lb = -Inf, ub = +Inf)

	# SUM x.i = 1
	constraints = add.constraints(rep(1, n), 1, type = '=', constraints)		

	ret = prices / mlag(prices) - 1
	weight = coredata(prices)
		weight[] = NA

	for( i in week.ends[week.ends >= (63 + 1)] ) {
		# one quarter is 63 days
		hist = ret[ (i- 63 +1):i, ]

		# create historical input assumptions
		ia = create.historical.ia(hist, 252)
			s0 = apply(coredata(hist),2,sd)		
			ia$cov = cor(coredata(hist), use='complete.obs',method='pearson') * (s0 %*% t(s0))

		weight[i,] = min.risk.portfolio(ia, constraints)
	}

	# Minimum Variance
	data$weight[] = weight		
		capital = 100000
		data$weight[] = (capital / prices) * data$weight
	min.var.daily = bt.run(data, type='share', capital=capital)

```

接下来让我们使用每周数据创建最小方差组合：

```

	#*****************************************************************
	# Code Strategies: Weekly
	#****************************************************************** 	
	retw = data.weekly$prices / mlag(data.weekly$prices) - 1
	weightw = coredata(prices)
		weightw[] = NA

	for( i in week.ends[week.ends >= (63 + 1)] ) {	
		# map
		j = which(index(ret[i,]) == index(retw))

		# one quarter = 13 weeks
		hist = retw[ (j- 13 +1):j, ]

		# create historical input assumptions
		ia = create.historical.ia(hist, 52)
			s0 = apply(coredata(hist),2,sd)		
			ia$cov = cor(coredata(hist), use='complete.obs',method='pearson') * (s0 %*% t(s0))

		weightw[i,] = min.risk.portfolio(ia, constraints)
	}	

	data$weight[] = weightw		
		capital = 100000
		data$weight[] = (capital / prices) * data$weight
	min.var.weekly = bt.run(data, type='share', capital=capital)

	#*****************************************************************
	# Create Report
	#****************************************************************** 
	plotbt.custom.report.part1(min.var.weekly, min.var.daily, equal.weight)

	# plot Daily and Weekly transition maps
	layout(1:2)
	plotbt.transition.map(min.var.daily$weight)
		legend('topright', legend = 'min.var.daily', bty = 'n')
	plotbt.transition.map(min.var.weekly$weight)
		legend('topright', legend = 'min.var.weekly', bty = 'n')

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot1-small2.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot2-small2.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot3-small2.png)

我发现使用每日收益构建输入假设创建的最小方差组合与使用每周收益构建输入假设创建的最小方差组合非常不同，这一不一致的一个可能解释在帕特·伯恩斯在[波动性谜团持续](http://www.portfolioprobe.com/2011/12/05/the-volatility-mystery-continues/)一文中进行了讨论。

以下是我建议您可以尝试使用此代码的几种方式：

+   使协方差矩阵估计更稳定，使用 tawny 包中的 Ledoit-Wolf 协方差收缩估计器

    ```

    ia$cov = tawny::cov.shrink(hist)

    ```

    或者

    ```

    ia$cov = cor(coredata(hist), use='complete.obs',method='spearman') * (s0 %*% t(s0))

    ```

    或者

    ```

    ia$cov = cor(coredata(hist), use='complete.obs',method='kendall') * (s0 %*% t(s0))

    ```

+   使用不同的投资范围

+   考虑不同的再平衡计划

+   考虑不同的风险度量。例如，在关于[资产配置](https://systematicinvestor.wordpress.com/category/asset-allocation/)系列文章中，我讨论并实施了以下风险度量：

    +   最小损失组合投资组合

    +   最小绝对偏差投资组合

    +   最小条件 VaR 投资组合

    +   最小条件 VaR 投资组合

    +   最小绝对偏差下行投资组合

    +   最小风险下行投资组合

要查看此示例的完整源代码，请查看[bt.test.r 中的 bt.min.var.test()函数在 github 上的链接](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
