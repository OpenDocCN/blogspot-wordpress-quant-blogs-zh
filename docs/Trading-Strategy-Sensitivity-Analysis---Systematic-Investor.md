<!--yml

分类：未分类

日期：2024-05-18 14:45:34

-->

# 交易策略敏感性分析 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2011/11/29/trading-strategy-sensitivity-analysis/#0001-01-01`](https://systematicinvestor.wordpress.com/2011/11/29/trading-strategy-sensitivity-analysis/#0001-01-01)

在设计交易策略时，我要确保策略参数的小幅变化不会将盈利的策略转变为亏损的策略。我将使用 David Varadi 在[Improving Trend-Following Strategies With Counter-Trend Entries](http://cssanalytics.wordpress.com/2011/07/29/improving-trend-following-strategies-with-counter-trend-entries/)一文中展示的示例策略，研究在不同参数情景下策略的鲁棒性和盈利性。

首先，让我们使用[Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)中的回测库来实现这个趋势追踪策略：

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
	tickers = spl('SPY')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)
	bt.prep(data, align='keep.all', dates='1970::2011')

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 
	prices = data$prices    

	# Buy & Hold	
	data$weight[] = 1
	buy.hold = bt.run(data)	

	# Trend-Following strategy: Long[Close > SMA(10) ]
	sma = bt.apply(data, function(x) { SMA(Cl(x), 10) } )	
	data$weight[] = NA
		data$weight[] = iif(prices >= sma, 1, 0)
	trend.following = bt.run(data, trade.summary=T)			

	# Trend-Following With Counter-Trend strategy: Long[Close > SMA(10), DVB(1) CounterTrend ]
	dv = bt.apply(data, function(x) { DV(HLC(x), 1, TRUE) } )	
	data$weight[] = NA
		data$weight[] = iif(prices > sma & dv < 0.25, 1, data$weight)
		data$weight[] = iif(prices < sma & dv > 0.75, 0, data$weight)
	trend.following.dv1 = bt.run(data, trade.summary=T)			

	#*****************************************************************
	# Create Report
	#****************************************************************** 
	plotbt.custom.report(trend.following.dv1, trend.following, buy.hold)	

```

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot1-small9.png)

![plot2.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot2-small8.png)

逆趋势入场（trend.following.dv1，黑线）提高了简单趋势追踪（trend.following，红线）策略的表现：两者回报更高，回撤更小。

接下来，我将检查 CAGR、Sharpe、DVR 和最大回撤如何受到移动平均长度从 10 到 100 变化和 DV 长度从 1 到 5 变化的影响：

```

	#*****************************************************************
	# Sensitivity Analysis
	#****************************************************************** 
	ma.lens = seq(10, 100, by = 10)
	dv.lens = seq(1, 5, by = 1)

	# precompute indicators
	mas = matrix(double(), nrow(prices), len(ma.lens))
	dvs = matrix(double(), nrow(prices), len(dv.lens))

	for(i in 1:len(ma.lens)) {
		ma.len = ma.lens[i]
		mas[, i] = bt.apply(data, function(x) { SMA(Cl(x), ma.len) } )
	}
	for(i in 1:len(dv.lens)) {
		dv.len = dv.lens[i]
		dvs[,i] = bt.apply(data, function(x) { DV(HLC(x), dv.len, TRUE) } )
	}

	# allocate matrixes to store backtest results
	dummy = matrix(double(), len(ma.lens), 1+len(dv.lens))
		rownames(dummy) = paste('SMA', ma.lens)
		colnames(dummy) = c('NO', paste('DV', dv.lens))

	out = list()
		out$Cagr = dummy
		out$Sharpe = dummy
		out$DVR = dummy
		out$MaxDD = dummy

	# evaluate strategies
	for(ima in 1:len(ma.lens)) {
		sma = mas[, ima]
		cat('SMA =', ma.lens[ima], '\n')

		for(idv in 0:len(dv.lens)) {			
			if( idv == 0 ) {
				data$weight[] = NA
					data$weight[] = iif(prices > sma, 1, 0)			
			} else {
				dv = dvs[, idv]

				data$weight[] = NA
					data$weight[] = iif(prices > sma & dv < 0.25, 1, data$weight)
					data$weight[] = iif(prices < sma & dv > 0.75, 0, data$weight)
			}
			strategy = bt.run(data, silent=T)

			# add 1 to account for benchmark case, no counter-trend
			idv = idv + 1
			out$Cagr[ima, idv] = compute.cagr(strategy$equity)
			out$Sharpe[ima, idv] = compute.sharpe(strategy$ret)
			out$DVR[ima, idv] = compute.DVR(strategy)
			out$MaxDD[ima, idv] = compute.max.drawdown(strategy$equity)
		}
	}

	#*****************************************************************
	# Create Report
	#****************************************************************** 
	layout(matrix(1:4,nrow=2))	
	for(i in names(out)) {
		temp = out[[i]]
		temp[] = plota.format( 100 * temp, 1, '', '' )
		plot.table(temp, smain = i, highlight = T, colorbar = F)
	}

```

![plot3.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot3-small6.png)

第一列，标签为“NO”，显示了趋势追踪策略（无逆趋势入场）的表现。逆趋势过滤器提高了大多数参数情景下策略的表现。这是进行敏感性分析所希望得到的结果，策略在多种参数下都是鲁棒且盈利的。

下一个步骤，你可以作为家庭作业来做，就是检查不同品种对策略表现的影响。例如，更具波动性的纳斯达克（QQQ），或者加拿大的标普/TSX 指数（XIU.TO）。

要查看这个示例的完整源代码，请查看[github](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)上的 bt.improving.trend.following.test()函数。
