<!--yml

category: 未分类

date: 2024-05-18 14:41:25

-->

# 借鉴自 Timely Portfolio | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/04/16/borrowing-ideas-from-timely-portfolio/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/04/16/borrowing-ideas-from-timely-portfolio/#0001-01-01)

我想突出显示我通过阅读[Timely Portfolio](http://timelyportfolio.blogspot.com)的精美博客发现的两种出色的可视化技术。

第一种方法是基于[使用新图表在日经上的 lm 系统](http://timelyportfolio.blogspot.ca/2011/08/lm-system-on-nikkei-with-new-chart.html)。让我们通过用绿色/红色/灰色突出显示底层（即买入和持有）来可视化策略的多头/空头/未投资时期。以下是使用[Systematic Investor Toolbox](https://github.com/systematicinvestor/SIT)实现此想法的示例代码。

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)
# https://systematicinvestor.wordpress.com/systematic-investor-toolbox/
###############################################################################
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')	
	tickers = spl('SPY')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)		
	bt.prep(data, align='keep.all', dates='2000::2011')

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 
	prices = data$prices    

	# Buy & Hold	
	data$weight[] = 1
	buy.hold = bt.run(data)	

	# Strategy
	ma10 = bt.apply.matrix(prices, EMA, 10)
	ma50 = bt.apply.matrix(prices, EMA, 50)
	ma200 = bt.apply.matrix(prices, EMA, 200)
	data$weight[] = NA;
		data$weight[] = iif(ma10 > ma50 & ma50 > ma200, 1, 
				iif(ma10 < ma50 & ma50 < ma200, -1, 0))
	strategy = bt.run.share(data, clean.signal=F)	

	#*****************************************************************
	# Visualization of system Entry and Exit based on
	# http://timelyportfolio.blogspot.ca/2011/08/lm-system-on-nikkei-with-new-chart.html
	#****************************************************************** 	
	layout(1)
	plota(strategy$eq, type='l', ylim=range(buy.hold$eq,strategy$eq))

	col = iif(strategy$weight > 0, 'green', iif(strategy$weight < 0, 'red', 'gray'))
	plota.lines(buy.hold$eq, type='l', col=col)			
		plota.legend('strategy,Long,Short,Not Invested','black,green,red,gray')		

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot1-small1.png)

我们可以从图中直观地确定策略的多头/空头/未投资时期。

另一种方法是基于[回撤可视化](http://timelyportfolio.blogspot.ca/2011/08/drawdown-visualization.html)。让我们通过以黄色突出显示回撤大于 10%的时期，大于 15%的时期以橙色突出显示来可视化回撤。

```

	#*****************************************************************	
	# Drawdown Visualization 
	# 10% drawdowns in yellow and 15% drawdowns in orange
	# http://timelyportfolio.blogspot.ca/2011/08/drawdown-visualization.html
	#*****************************************************************	
	layout(1:2)
	drawdowns = compute.drawdown(strategy$eq)
	highlight = drawdowns < -0.1

	plota.control$col.x.highlight = iif(drawdowns < -0.15, 'orange', iif(drawdowns < -0.1, 'yellow', 0))	

	plota(strategy$eq, type='l', plotX=F, x.highlight = highlight, ylim=range(buy.hold$eq,strategy$eq))
		plota.legend('strategy,10% Drawdown,15%  Drawdown','black,yellow,orange')

	plota(100*drawdowns, type='l', x.highlight = highlight)
		plota.legend('drawdown', 'black', x='bottomleft')

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot2-small1.png)

下一个逻辑步骤是在回测图中引入突出显示。这非常容易做到，因为我使用 plota 库创建回测报告。

```

	#*****************************************************************
	# Create Report
	#****************************************************************** 		
	plota.control$col.x.highlight = iif(drawdowns < -0.15, 'orange', iif(drawdowns < -0.1, 'yellow', 0))				
	highlight = drawdowns < -0.1

	plotbt.custom.report.part1(strategy, buy.hold, x.highlight = highlight)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot3-small1.png)

请告诉我您使用的其他可视化技术。

要查看此示例的完整源代码，请查看 [github 上的 bt.timelyportfolio.visualization.test() 函数在 bt.test.r 中](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
