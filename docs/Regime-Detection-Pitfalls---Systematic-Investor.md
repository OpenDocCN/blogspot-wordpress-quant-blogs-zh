<!--yml

类别：未分类

日期：2024-05-18 14:35:56

-->

# 政权检测陷阱 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/11/15/regime-detection-pitfalls/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/11/15/regime-detection-pitfalls/#0001-01-01)

今天，我想回答一些关于[政权检测](https://systematicinvestor.wordpress.com/2012/11/01/regime-detection/)帖子的问题。在[政权检测](https://systematicinvestor.wordpress.com/2012/11/01/regime-detection/)帖子中，我举了一个基于模拟数据的例子，有些朋友尝试将这个例子应用于实际股票。

在设计使用[政权检测](https://systematicinvestor.wordpress.com/2012/11/01/regime-detection/)的交易系统时，有一个很大的问题你需要注意。让我用一个简单的例子来演示。

假设我们使用了 SPY 10 年的日收益数据来训练我们的模型（两种政权：牛市和熊市）。接下来，我们用样本外数据测试一个策略，在牛市政权下持有多头头寸，在熊市政权下持有现金头寸。感谢 systematicedge.wordpress.com 的 Michael Guan 提出这个问题。

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
	data <- new.env()
	getSymbols('SPY', src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)
		data$SPY = adjustOHLC(data$SPY, use.Adjusted=T)							
	bt.prep(data)

	#*****************************************************************
	# Setup
	#****************************************************************** 		
	nperiods = nrow(data$prices)

	models = list()

	rets = ROC(Ad(data$SPY))
		rets[1] = 0

	# use 10 years: 1993:2002 for training	
	in.sample.index = '1993::2002'
	out.sample.index = '2003::'

	in.sample = rets[in.sample.index]
	out.sample = rets[out.sample.index]
	out.sample.first.date = nrow(in.sample) + 1

	#*****************************************************************
	# Fit Model
	#****************************************************************** 		
	load.packages('RHmm')	
	fit = HMMFit(in.sample, nStates=2)

	# find states
	states.all = rets * NA
	states.all[] = viterbi(fit, rets)$states

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 
	data$weight[] = NA
		data$weight[] = iif(states.all == 1, 0, 1)
		data$weight[in.sample.index] = NA
	models$states.all = bt.run.share(data)

	# create plot
	plotbt.custom.report.part1(models) 

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/11/plot1-small1.png)

这些结果对于这样一个简单的策略来说好得不太真实。你在 10 年内用最小的跌幅进行了投资。那么问题在哪里？

维特比算法（[Viterbi algorithm](http://en.wikipedia.org/wiki/Viterbi_algorithm)）使用所有数据来计算最可能的序列状态。即在上面的代码中，我们将所有日期的回报传递给维特比算法（[Viterbi algorithm](http://en.wikipedia.org/wiki/Viterbi_algorithm)）。因此，例如，维特比算法（[Viterbi algorithm](http://en.wikipedia.org/wiki/Viterbi_algorithm)）可能会使用 2008 年的数据来确定 2007 年的状态。这是一个很大的问题，我们可以通过滚动窗口方法来解决。不幸的是，我们的预测准确性和策略回报准确性会下降。

```

	#*****************************************************************
	# Find problem - results are too good
	#****************************************************************** 		
	# The viterbi function need to see all data to compute the most likely sequence of states
	# http://en.wikipedia.org/wiki/Viterbi_algorithm

	# We can use expanding window to determine the states
	states.win1 = states.all * NA
	for(i in out.sample.first.date:nperiods) {
		states.win1[i] = last(viterbi(fit, rets[1:i])$states)
		if( i %% 100 == 0) cat(i, 'out of', nperiods, '\n')
	}

	# Or we can refit model over expanding window as suggested in the
	# Regime Shifts: Implications for Dynamic Strategies by M. Kritzman, S. Page, D. Turkington
	# Out-of-Sample Analysis, page 8
	initPoint = fit$HMM
	states.win2 = states.all * NA
	for(i in out.sample.first.date:nperiods) {
		fit2 = HMMFit(rets[2:i], nStates=2, control=list(init='USER', initPoint = initPoint))
			initPoint = fit2$HMM
		states.win2[i] = last(viterbi(fit2, rets[2:i])$states)
		if( i %% 100 == 0) cat(i, 'out of', nperiods, '\n')
	}

	#*****************************************************************
	# Plot States
	#****************************************************************** 			
	layout(1:3)
	col = col.add.alpha('white',210)
	plota(states.all[out.sample.index], type='s', plotX=F)
		plota.legend('Implied States based on all data', x='center', bty='o', bg=col, box.col=col,border=col,fill=col,cex=2)
	plota(states.win1[out.sample.index], type='s')
		plota.legend('Implied States based on rolling window', x='center', bty='o', bg=col, box.col=col,border=col,fill=col,cex=2)
	plota(states.win2[out.sample.index], type='s')
		plota.legend('Implied States based on rolling window(re-fit)', x='center', bty='o', bg=col, box.col=col,border=col,fill=col,cex=2)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/11/plot2-small1.png)

使用滚动窗口方法，状态变化得更频繁。我们可能需要添加一个过滤器，只有在一定数量的观察确认状态变化时才允许状态变化。即延迟状态变化，我们留到另一篇文章中讨论。

让我们来看看滚动窗口方法对回测结果的影响：

```

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 		
	data$weight[] = NA
		data$weight[] = iif(states.win1 == 1, 0, 1)
		data$weight[in.sample.index] = NA
	models$states.win1 = bt.run.share(data)

	data$weight[] = NA
		data$weight[] = iif(states.win2 == 1, 0, 1)
		data$weight[in.sample.index] = NA
	models$states.win2 = bt.run.share(data)

	#*****************************************************************
	# Create report
	#****************************************************************** 			
	plotbt.custom.report.part1(models) 

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/11/plot3-small.png)

正如预期的那样，将[政权检测](https://systematicinvestor.wordpress.com/2012/11/01/regime-detection/)应用于股票是相当困难的。

要查看此例子的完整源代码，请查看[bt.regime.detection.pitfalls.test()函数在 github 上的 bt.test.r](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
