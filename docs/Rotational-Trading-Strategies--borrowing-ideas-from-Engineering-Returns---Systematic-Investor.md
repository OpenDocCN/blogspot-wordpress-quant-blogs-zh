<!--yml

类别：未分类

日期：2024-05-18 14:44:28

-->

# 旋转交易策略：借鉴工程回报的想法 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2011/12/20/rotational-trading-strategies-borrowing-ideas-from-engineering-returns/#0001-01-01`](https://systematicinvestor.wordpress.com/2011/12/20/rotational-trading-strategies-borrowing-ideas-from-engineering-returns/#0001-01-01)

[工程回报](http://engineering-returns.com)博客的 Frank Hassler 写了一篇优秀的文章[轮换交易：如何减少交易并提高回报率](http://engineering-returns.com/2011/07/06/rotational-trading-how-to-reducing-trades-and-improve-returns/)。 文章提出了四种减少交易的方法：

+   减少交易频率。 即每周重新平衡而不是每日重新平衡。

+   不同的进入/退出交易标准。

+   平滑排名在过去几个条中的变化。

+   上述方法的组合。

我想展示如何使用[系统投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)中的回测库来实现这些想法。 我将使用[ETF 行业战略](http://www.etfscreen.com/sectorstrategy.php)帖子中的 21 个 ETF 作为投资范围。

以下代码从 Yahoo Finance 加载历史价格，并使用[系统投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)中的回测库比较每日与每周重新平衡的表现：

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
	tickers = spl('XLY,XLP,XLE,XLF,XLV,XLI,XLB,XLK,XLU,IWB,IWD,IWF,IWM,IWN,IWO,IWP,IWR,IWS,IWV,IWW,IWZ')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)		
	bt.prep(data, align='remove.na', dates='1970::2011')

	#*****************************************************************
	# Code Strategies : weekly rebalancing
	#****************************************************************** 
	prices = data$prices  
	n = len(tickers)  

	# find week ends
	week.ends = endpoints(prices, 'weeks')
		week.ends = week.ends[week.ends > 0]		

	# Rank on ROC 200
	position.score = prices / mlag(prices, 200)	
		position.score.ma = position.score		
		buy.rule = T

	# Select Top 2 funds daily
	data$weight[] = NA
		data$weight[] = ntop(position.score, 2)	
		capital = 100000
		data$weight[] = (capital / prices) * bt.exrem(data$weight)				
	top2.d = bt.run(data, type='share', trade.summary=T, capital=capital)

	# Select Top 2 funds weekly
	data$weight[] = NA
		data$weight[week.ends,] = ntop(position.score[week.ends,], 2)	
		capital = 100000
		data$weight[] = (capital / prices) * bt.exrem(data$weight)		
	top2.w = bt.run(data, type='share', trade.summary=T, capital=capital)

	# Plot Strategy Metrics Side by Side
	plotbt.strategy.sidebyside(top2.d, top2.w, perfromance.fn = 'engineering.returns.kpi')	

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot1-small4.png)

随着我们从每日重新平衡转换为每周重新平衡，交易次数从 443 下降到 164。 额外的好处是每周重新平衡的更好回报。

接下来，让我们检查不同的入场/出场排名。 我们将购买排名前 2 位的 ETF，并将它们保持在排名低于 4/6 之前。

```

	#*****************************************************************
	# Code Strategies : different entry/exit rank
	#****************************************************************** 

	# Select Top 2 funds, Keep till they are in 4/6 rank
	data$weight[] = NA
		data$weight[] = ntop.keep(position.score, 2, 4)	
		capital = 100000
		data$weight[] = (capital / prices) * bt.exrem(data$weight)		
	top2.d.keep4 = bt.run(data, type='share', trade.summary=T, capital=capital)

	data$weight[] = NA
		data$weight[] = ntop.keep(position.score, 2, 6)	
		capital = 100000
		data$weight[] = (capital / prices) * bt.exrem(data$weight)		
	top2.d.keep6 = bt.run(data, type='share', trade.summary=T, capital=capital)

	# Plot Strategy Metrics Side by Side
	plotbt.strategy.sidebyside(top2.d, top2.d.keep4, top2.d.keep6, perfromance.fn = 'engineering.returns.kpi')

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot2-small4.png)

随着我们将选择保持更长时间段，交易次数从 443 下降到 95 到 52。

接下来，让我们检查排名平滑。 我们将不再使用最近的排名，而是使用排名最近值的不同平均值。

```

	#*****************************************************************
	# Code Strategies : Rank smoothing
	#****************************************************************** 

	models = list()
	models$Bench = top2.d
	for( avg in spl('SMA,EMA') ) {
		for( i in c(3,5,10,20) ) {		
			position.score.smooth = bt.apply.matrix(position.score.ma, avg, i)	
				position.score.smooth[!buy.rule,] = NA

			data$weight[] = NA
				data$weight[] = ntop(position.score.smooth, 2)	
				capital = 100000
				data$weight[] = (capital / prices) * bt.exrem(data$weight)		
			models[[ paste(avg,i) ]] = bt.run(data, type='share', trade.summary=T, capital=capital)		
		}
	}

	# Plot Strategy Metrics Side by Side
	plotbt.strategy.sidebyside(models, perfromance.fn = 'engineering.returns.kpi')

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot3-small4.png)

随着我们在平均值中使用的周期长度增加，交易次数下降。 使用简单移动平均（SMA）与指数平滑平均（EMA）没有太大区别。

接下来，让我们组合不同的方法来减少交易次数。

```

	#*****************************************************************
	# Code Strategies : Combination
	#****************************************************************** 

	# Select Top 2 funds daily, Keep till they are 6 rank, Smooth Rank by 10 day EMA
	position.score.smooth = bt.apply.matrix(position.score.ma, 'EMA', 10)	
		position.score.smooth[!buy.rule,] = NA
	data$weight[] = NA
		data$weight[] = ntop.keep(position.score.smooth, 2, 6)	
		capital = 100000
		data$weight[] = (capital / prices) * bt.exrem(data$weight)		
	top2.d.keep6.EMA10 = bt.run(data, type='share', trade.summary=T, capital=capital)

	# Select Top 2 funds weekly, Keep till they are 6 rank
	data$weight[] = NA
		data$weight[week.ends,] = ntop.keep(position.score[week.ends,], 2, 6)	
		capital = 100000
		data$weight[] = (capital / prices) * bt.exrem(data$weight)		
	top2.w.keep6 = bt.run(data, type='share', trade.summary=T, capital=capital)

	# Select Top 2 funds weekly, Keep till they are 6 rank, Smooth Rank by 10 week EMA
	position.score.smooth[] = NA
		position.score.smooth[week.ends,] = bt.apply.matrix(position.score.ma[week.ends,], 'EMA', 10)	
			position.score.smooth[!buy.rule,] = NA

	data$weight[] = NA
		data$weight[week.ends,] = ntop.keep(position.score.smooth[week.ends,], 2, 6)	
		capital = 100000
		data$weight[] = (capital / prices) * bt.exrem(data$weight)		
	top2.w.keep6.EMA10 = bt.run(data, type='share', trade.summary=T, capital=capital)

	# Plot Strategy Metrics Side by Side
	plotbt.strategy.sidebyside(top2.d, top2.d.keep6, top2.d.keep6.EMA10, top2.w, top2.w.keep6, top2.w.keep6.EMA10, perfromance.fn = 'engineering.returns.kpi')

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot4-small2.png)

总体胜出者是一种每周策略，该策略基于 10 周指数平均排名购买排名前 2 的 ETF，并持有它们直到它们的排名降至 6 以下。交易次数从 443 下降到 28，表现（年化复合增长率）从 2.4%上升到 7.3%。

下一个步骤，你可以作为家庭作业来做，就是寻找控制策略回撤的方法。一个解决方案在[避免严重回撤](http://engineering-returns.com/2010/07/26/rotational-trading-system/)这篇文章中讨论。

要查看这个示例的完整源代码，请查看 GitHub 上的[bt.rotational.trading.trades.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
