<!--yml

category: 未分类

date: 2024-05-18 14:44:52

-->

# 再平衡方法的历史回测 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2011/12/16/backtesting-rebalancing-methods/#0001-01-01`](https://systematicinvestor.wordpress.com/2011/12/16/backtesting-rebalancing-methods/#0001-01-01)

我在[资产配置流程总结](https://systematicinvestor.wordpress.com/2011/11/22/asset-allocation-process-summary/)帖子中谈到了再平衡。决定何时如何再平衡（更新投资组合至目标配置）是资产配置流程中的关键步骤之一。我想研究以下再平衡方法的投资组合表现和[周转率](http://wiki.fool.com/Portfolio_turnover)：

+   定期再平衡: 每月、季度、年度向**目标配置**再平衡。

+   最大偏差再平衡: 当资产权重偏离目标一定百分比时，再平衡至**目标配置**。

+   最大偏差再平衡: 当资产权重偏离目标配置一定百分比时，再平衡**一半到目标配置**。

我将研究一个非常简单的目标配置：50%配置给股票（[SPY](http://www.google.com/finance?q=spy)）和 50%配置给固定收益（[TLT](http://www.google.com/finance?q=tlt)）。

首先，让我们研究定期再平衡。以下代码使用[系统投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)中的回测库来实现该策略：

```

# Load Systematic Investor Toolbox (SIT)
setInternet2(TRUE)
con = gzcon(url('https://github.com/systematicinvestor/SIT/raw/master/sit.gz', 'rb'))
	source(con)
close(con)

	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')
	tickers = spl('SPY,TLT')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1900-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)
	bt.prep(data, align='remove.na', dates='1900::2011')

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 
	prices = data$prices   
	nperiods = nrow(prices)
	target.allocation = matrix(c(0.5, 0.5), nrow=1)

	# Buy & Hold	
	data$weight[] = NA	
		data$weight[1,] = target.allocation
		capital = 100000
		data$weight[] = (capital / prices) * data$weight
	buy.hold = bt.run(data, type='share', capital=capital)

	# Rebalance periodically
	models = list()
	for(period in spl('months,quarters,years')) {
		data$weight[] = NA	
			data$weight[1,] = target.allocation

			period.ends = endpoints(prices, period)
				period.ends = period.ends[period.ends > 0]		
			data$weight[period.ends,] = repmat(target.allocation, len(period.ends), 1)

			capital = 100000
			data$weight[] = (capital / prices) * data$weight
		models[[period]] = bt.run(data, type='share', capital=capital)	
	}
	models$buy.hold = buy.hold				

	#*****************************************************************
	# Create Report
	#****************************************************************** 		
	plotbt.custom.report(models)		

	# Plot BuyHold and Monthly Rebalancing Weights
	layout(1:2)
	plotbt.transition.map(models$buy.hold$weight, 'buy.hold', spl('red,orange'))
		abline(h=50)
	plotbt.transition.map(models$months$weight, 'months', spl('red,orange'))
		abline(h=50)

	# helper function to create barplot with labels
	barplot.with.labels <- function(data, main, plotX = TRUE) {
		par(mar=c( iif(plotX, 6, 2), 4, 2, 2))
		x = barplot(100 * data, main = main, las = 2, names.arg = iif(plotX, names(data), ''))
		text(x, 100 * data, round(100 * data,1), adj=c(0.5,1), xpd = TRUE)
	}
	# Plot Portfolio Turnover for each Rebalancing method
	layout(1)
	barplot.with.labels(sapply(models, compute.turnover, data), 'Average Annual Portfolio Turnover')

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot1-small3.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot2-small3.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot3-small3.png)

如预期的那样，买入并持有策略的周转率为 0，但与目标配置相差甚远。另一方面，每月再平衡会使投资组合保持接近目标配置，但代价是 36%的年度周转率。

下一步触发基于与目标配置的最大偏差再平衡，我创建了一个函数 bt.max.deviation.rebalancing，它迭代搜索最大偏差的违反，并一旦违法发生就强制再平衡。该函数可以根据再平衡比率全部或部分地将投资组合再平衡到目标配置。例如，对于再平衡比率等于 0，每当发现最大偏差的违反时，投资组合都会完全再平衡到目标配置，对于再平衡比率等于 0.5，投资组合会再平衡到目标配置的一半。

```

# Rebalancing method based on maximum deviation
bt.max.deviation.rebalancing <- function
(
	data, 
	model, 
	target.allocation, 
	max.deviation = 3/100, 
	rebalancing.ratio = 0	# 0 means rebalance all-way to target.allocation
				# 0.5 means rebalance half-way to target.allocation
) 
{
	start.index = 1
	nperiods = nrow(model$weight)
	action.index = rep(F, nperiods)

	while(T) {	
		# find rows that violate max.deviation
		weight = model$weight
		index = which( apply(abs(weight - repmat(target.allocation, nperiods, 1)), 1, max) > max.deviation)	

		if( len(index) > 0 ) {
			index = index[ index > start.index ]

			if( len(index) > 0 ) {
				action.index[index[1]] = T

				data$weight[] = NA	
					data$weight[1,] = target.allocation

					temp = repmat(target.allocation, sum(action.index), 1)
					data$weight[action.index,] = temp + 
						rebalancing.ratio * (weight[action.index,] - temp)					

					capital = 100000
					data$weight[] = (capital / data$prices) * data$weight
				model = bt.run(data, type='share', capital=capital, silent=T)	
				start.index = index[1]
			} else break			
		} else break		
	}
	return(model)
}

```

现在，让我们将 5%最大偏差再平衡与定期再平衡进行比较。

```

	#*****************************************************************
	# Code Strategies that rebalance based on maximum deviation
	#****************************************************************** 

	# rebalance to target.allocation when portfolio weights are 5% away from target.allocation
	models$smart5.all = bt.max.deviation.rebalancing(data, buy.hold, target.allocation, 5/100, 0) 

	# rebalance half-way to target.allocation when portfolio weights are 5% away from target.allocation
	models$smart5.half = bt.max.deviation.rebalancing(data, buy.hold, target.allocation, 5/100, 0.5) 

	#*****************************************************************
	# Create Report
	#****************************************************************** 						
	# Plot BuyHold, Years and Max Deviation Rebalancing Weights	
	layout(1:4)
	plotbt.transition.map(models$buy.hold$weight, 'buy.hold', spl('red,orange'))
		abline(h=50)
	plotbt.transition.map(models$smart5.all$weight, 'Max Deviation 5%, All the way', spl('red,orange'))
		abline(h=50)
	plotbt.transition.map(models$smart5.half$weight, 'Max Deviation 5%, Half the way', spl('red,orange'))
		abline(h=50)
	plotbt.transition.map(models$years$weight, 'years', spl('red,orange'))
		abline(h=50)

	# Plot Portfolio Turnover and Maximum Deviation for each Rebalancing method
	layout(1:2)
	barplot.with.labels(sapply(models, compute.turnover, data), 'Average Annual Portfolio Turnover', F)
	barplot.with.labels(sapply(models, compute.max.deviation, target.allocation), 'Maximum Deviation from Target Mix')

	# Plot Strategy Statistics  Side by Side
	plotbt.strategy.sidebyside(models)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot4-small1.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot5-small1.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot6-small1.png)

如预期的那样，最大偏差再平衡使投资组合保持接近目标混合。此外，最大偏差再平衡策略的换手率低于月度再平衡。因此，在这种情况下，最大偏差再平衡胜过周期性再平衡方法。

要查看此示例的完整源代码，请查看[github 上的 bt.test.r 中的 bt.rebalancing.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
