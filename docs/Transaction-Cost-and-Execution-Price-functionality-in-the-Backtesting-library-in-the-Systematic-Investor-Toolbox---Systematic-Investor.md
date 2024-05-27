<!--yml

category: 未分类

date: 2024-05-18 14:41:33

-->

# 系统投资者工具箱中的回测库的交易成本和执行价格功能 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/04/03/transaction-cost-and-execution-price-functionality-in-the-backtesting-library-in-the-systematic-investor-toolbox/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/04/03/transaction-cost-and-execution-price-functionality-in-the-backtesting-library-in-the-systematic-investor-toolbox/#0001-01-01)

我想介绍系统投资者工具箱（[Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)）中回测库的交易成本（[Transaction Cost](http://en.wikipedia.org/wiki/Transaction_cost)）和执行价格（Execution Price）功能。

交易成本是通过 bt.run()函数中的佣金参数实现的。对于“股票”类型的回测，您可以指定每股的佣金金额；对于“权重”类型的回测，您可以将佣金指定为总交易额的百分比。

下面是一个简单的 50/200 日均线交叉策略示例，每股交易费用为 10 美分：

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
	bt.prep(data, align='keep.all', dates='1970::')	

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 
	prices = data$prices   
	nperiods = nrow(prices)

	models = list()

	#*****************************************************************
	# Buy & Hold
	#****************************************************************** 
	data$weight[] = 0
		data$execution.price[] = NA
		data$weight[] = 1
	models$buy.hold = bt.run.share(data, clean.signal=T)

	#*****************************************************************
	# MA cross-over strategy
	#****************************************************************** 
	sma.fast = SMA(prices, 50)
	sma.slow = SMA(prices, 200)
		signal = iif(sma.fast >= sma.slow, 1, -1)

	data$weight[] = NA
		data$weight[] = signal
	models$ma.crossover = bt.run.share(data, clean.signal=T, trade.summary = TRUE)

	#*****************************************************************
	# MA cross-over strategy, add 10c per share commission
	#*****************************************************************	
	data$weight[] = NA
		data$weight[] = signal
	models$ma.crossover.com = bt.run.share(data, commission = 0.10, clean.signal=T)

```

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot1-small.png)

交易成本将总体策略表现从 5.13 降低到了 4.83

系统投资者工具箱中的回测库默认假设每天的交易只有一个价格，我默认使用收盘价。执行价格（Execution.Price）字段允许覆盖这个默认功能。在以下示例中，我将 50/200 日均线交叉策略修改为在信号发出次日开盘时进入交易。

```

	#*****************************************************************
	# MA cross-over strategy:
	# Exit trades at the close on the day of the signal
	# Enter trades at the open the next day after the signal	
	#****************************************************************** 
	popen = bt.apply(data, Op)		
	signal.new = signal
		trade.start	 = which(signal != mlag(signal) & signal != 0)
		signal.new[trade.start] = 0
		trade.start = trade.start + 1

	data$weight[] = NA
		data$execution.price[] = NA
		data$execution.price[trade.start,] = popen[trade.start,]
		data$weight[] = signal.new
	models$ma.crossover.enter.next.open = bt.run.share(data, clean.signal=T, trade.summary = TRUE)			

	#*****************************************************************
	# Create Report
	#****************************************************************** 	
	# Plot perfromance
	plotbt(models, plotX = T, log = 'y', LeftMargin = 3)	    	
		mtext('Cumulative Performance', side = 2, line = 1)

	# Plot trades
	plotbt.custom.report.part3(models$ma.crossover, trade.summary = TRUE)		
	plotbt.custom.report.part3(models$ma.crossover.enter.next.open, trade.summary = TRUE)		

```

这个修改将总体策略表现从 5.13 降低到了 5.09，我们可以通过比较每个策略下的交易来重新检查逻辑：

![plot2.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot2-small.png)

![plot3.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/plot3-small.png)

要查看这个示例的完整源代码，请查看[bt.execution.price.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
