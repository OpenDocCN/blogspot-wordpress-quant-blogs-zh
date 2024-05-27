<!--yml

category: 未分类

date: 2024-05-18 14:33:18

-->

# 最大夏普投资组合 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2013/03/22/maximum-sharpe-portfolio/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/03/22/maximum-sharpe-portfolio/#0001-01-01)

最大夏普投资组合或正切投资组合是[有效前沿](http://en.wikipedia.org/wiki/Efficient_frontier)上的投资组合，在点（0，无风险利率）画出的直线与[有效前沿](http://en.wikipedia.org/wiki/Efficient_frontier)相切的点。

在[quadprog optimization](http://stackoverflow.com/questions/10526243/quadprog-optimization)的问题中有关于最大夏普投资组合或正切投资组合的很好的讨论。一般情况下，找到最大夏普投资组合需要一个非线性求解器，因为我们想要找到投资组合权重 `w` 来最大化 `w' mu / sqrt( w' V w )`（即[夏普比率](http://www.stanford.edu/~wfsharpe/art/sr/sr.htm)是 `w` 的非线性函数）。但是，如在[quadprog optimization](http://stackoverflow.com/questions/10526243/quadprog-optimization)的问题中讨论的，存在特殊的情况可以使用二次求解器来找到最大夏普投资组合。只要所有约束的齐次度为 0（即，如果我们将 `w` 乘以一个数，约束不变化– 例如，w1 > 0 相当于 5*w1 > 5*0 ），就可以使用二次求解器来找到最大夏普投资组合或正切投资组合。

我已经在 [github 的 strategy.r 中实现了找到最大夏普投资组合或正切投资组合的逻辑](https://github.com/systematicinvestor/SIT/blob/master/R/strategy.r)。您可以指定以下 2 个参数：

+   投资组合类型：‘仅多头’、‘多头-空头’或‘市场中性’

+   投资组合曝光。例如，“仅多头”（‘long-only’）的曝光 = 1，是一个完全投资的投资组合

现在，让我们构建一个样本[有效前沿](http://en.wikipedia.org/wiki/Efficient_frontier)，并绘制最大夏普投资组合。

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
	# Create Efficient Frontier
	#****************************************************************** 	
	# create sample historical input assumptions
	ia = aa.test.create.ia()

	# create long-only, fully invested efficient frontier
	n = ia$n		

	# 0 <= x.i <= 1
	constraints = new.constraints(n, lb = 0, ub = 1)
		constraints = add.constraints(diag(n), type='>=', b=0, constraints)
		constraints = add.constraints(diag(n), type='<=', b=1, constraints)

	# SUM x.i = 1
	constraints = add.constraints(rep(1, n), 1, type = '=', constraints)		

	# create efficient frontier
	ef = portopt(ia, constraints, 50, 'Efficient Frontier') 

	#*****************************************************************
	# Create Plot
	#****************************************************************** 	
	# plot efficient frontier
	plot.ef(ia, list(ef), transition.map=F)	 

	# find maximum sharpe portfolio
	max(portfolio.return(ef$weight,ia) /  portfolio.risk(ef$weight,ia))

	# plot minimum variance portfolio
	weight = min.var.portfolio(ia,constraints)	
	points(100 * portfolio.risk(weight,ia), 100 * portfolio.return(weight,ia), pch=15, col='red')
	portfolio.return(weight,ia) /  portfolio.risk(weight,ia)

	# plot maximum Sharpe or tangency portfolio
	weight = max.sharpe.portfolio()(ia,constraints)	
	points(100 * portfolio.risk(weight,ia), 100 * portfolio.return(weight,ia), pch=15, col='orange')
	portfolio.return(weight,ia) /  portfolio.risk(weight,ia)

	plota.legend('Minimum Variance,Maximum Sharpe','red,orange', x='topright')	

```

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/03/plot1-small1.png)

现在让我们看看如何构建‘仅多头’、‘多头-空头’或‘市场中性’最大夏普投资组合或正切投资组合：

```

	#*****************************************************************
	# Examples of Maximum Sharpe or Tangency portfolios construction
	#****************************************************************** 	
	weight = max.sharpe.portfolio('long-only')(ia,constraints)	
		round(weight,2)
		round(c(sum(weight[weight<0]), sum(weight[weight>0])),2)

	weight = max.sharpe.portfolio('long-short')(ia,constraints)			
		round(weight,2)
		round(c(sum(weight[weight<0]), sum(weight[weight>0])),2)

	weight = max.sharpe.portfolio('market-neutral')(ia,constraints)			
		round(weight,2)
		round(c(sum(weight[weight<0]), sum(weight[weight>0])),2)	

```

预期的仅多头最大夏普投资组合的曝光为 100%。多头-空头最大夏普投资组合为多头 227%，空头 127%。市场中性最大夏普投资组合为多头 100%，空头 100%。

作为最后一步，我在 [适应性资产配置](https://systematicinvestor.wordpress.com/2012/08/14/adaptive-asset-allocation/) 帖子中使用了 10 个资产组合的最大夏普算法与我之前讨论过的其他投资组合优化方法进行了比较（即风险平价、最小方差、最大多样化、最小相关性）。

```

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

 	#*****************************************************************
	# Code Strategies
	#******************************************************************
	# find period ends
	period.ends = endpoints(prices, 'months')
        period.ends = period.ends[period.ends > 0]

	n.mom = 180
	n.vol = 60
	n.top = 4        
	momentum = prices / mlag(prices, n.mom)  

	obj = portfolio.allocation.helper(data$prices, period.ends=period.ends,
		lookback.len = n.vol, universe = ntop(momentum[period.ends,], n.top) > 0,
		min.risk.fns = list(EW=equal.weight.portfolio,
						RP=risk.parity.portfolio,
						MV=min.var.portfolio,
						MD=max.div.portfolio,
						MC=min.corr.portfolio,
						MC2=min.corr2.portfolio,
						MCE=min.corr.excel.portfolio,
						MS=max.sharpe.portfolio())
	) 

	models = create.strategies(obj, data)$models

	#*****************************************************************
	# Create Report
	#******************************************************************    
	strategy.performance.snapshoot(models, T)

	plotbt.custom.report.part2(models$MS)

	# Plot Portfolio Turnover for each strategy
	layout(1)
	barplot.with.labels(sapply(models, compute.turnover, data), 'Average Annual Portfolio Turnover')

```

使用最大夏普比率组合进行资产配置产生的组合更为集中，具有更高的总回报、更高的夏普比率和更高的换手率。

![plot2.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/03/plot2-small.png)

![plot3.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/03/plot3-small.png)

![plot4.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/03/plot4-small.png)
