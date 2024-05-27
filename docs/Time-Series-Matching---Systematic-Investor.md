<!--yml

类别：未分类

日期：2024-05-18 14:43:40

-->

# 时间序列匹配 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/01/13/time-series-matching/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/01/13/time-series-matching/#0001-01-01)

这不是投资建议。 本信息仅供参考。

[如果它看起来像鸭子，游得像鸭子，叫得像鸭子，那么它很可能就是鸭子。](http://en.wikipedia.org/wiki/Duck_test)

你想知道标普 500 在未来一周、一个月、一个季度会怎样吗？ 一种方法是通过找到与当前市场环境相似的历史时期，并检查发生了什么。 我将这个过程称为时间序列匹配，但你可能会找到与技术模式和分形相似的类似技术。 为了了解分形的味道，以下是两篇我最近阅读关于分形的文章：

我建议阅读以下关于时间序列匹配的文章来了解不同的方法：

我将使用[Jean-Robert Avettand-Fenoel](http://www.londonr.org/Sep%2011%20LondonR_AvettandJR.pdf)文章中概述的简单方法来寻找与 SPY 最近 90 天相似的时间序列匹配。

以下代码从雅虎财经加载历史价格，设置问题，并使用[系统投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)计算历史滚动窗口的欧几里得距离：

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)
###############################################################################
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')	
	tickers = 'SPY'

	data = getSymbols(tickers, src = 'yahoo', from = '1950-01-01', auto.assign = F)

	#*****************************************************************
	# Setup search
	#****************************************************************** 
	data = last(data, 252*10)
	reference = coredata(Cl(data))
		n = len(reference)
		query = reference[(n-90+1):n]	
		reference = reference[1:(n-90)]

		n.query = len(query)
		n.reference = len(reference)

	#*****************************************************************
	# Compute Distances
	#****************************************************************** 		
	dist = rep(NA, n.reference)
	query.normalized = (query - mean(query)) / sd(query)

	for( i in n.query : n.reference ) {
		window = reference[ (i - n.query + 1) : i]
		window.normalized = (window - mean(window)) / sd(window)
		dist[i] = stats:::dist(rbind(query.normalized, window.normalized))
	}

```

接下来，让我们在 SPY 历史中选择与“查询”模式最相似的 10 个匹配项：

```

	#*****************************************************************
	# Find Matches
	#****************************************************************** 			
	min.index = c()
	n.match = 10

	# only look at the minimums 
	temp = dist
		temp[ temp > mean(dist, na.rm=T) ] = NA

	# remove n.query, points to the left/right of the minimums
	for(i in 1:n.match) {
		if(any(!is.na(temp))) {
			index = which.min(temp)
			min.index[i] = index
			temp[max(0,index - 2*n.query) : min(n.reference,(index + n.query))] = NA
		}
	}
	n.match = len(min.index)

	#*****************************************************************
	# Plot Matches
	#****************************************************************** 		
	dates = index(data)[1:len(dist)]

	par(mar=c(2, 4, 2, 2))
	plot(dates, dist, type='l',col='gray', main='Top Matches', ylab='Euclidean Distance', xlab='')
		abline(h = mean(dist, na.rm=T), col='darkgray', lwd=2)
		points(dates[min.index], dist[min.index], pch=22, col='red', bg='red')
		text(dates[min.index], dist[min.index], 1:n.match, adj=c(1,1), col='black',xpd=TRUE)

	plota(data, type='l', col='gray', main=tickers)
		plota.lines(last(data,90), col='blue')
		for(i in 1:n.match) {
		plota.lines(data[(min.index[i]-n.query + 1):min.index[i]], col='red')
		}
		text(index(data)[min.index - n.query/2], reference[min.index - n.query/2], 1:n.match, 
			adj=c(1,-1), col='black',xpd=TRUE)
		plota.legend('Pattern,Match #','blue,red')

```

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/01/plot1-small1.png)

![plot2.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/01/plot2-small1.png)

接下来，让我们将所有匹配项与“查询”模式叠加，并在匹配发生后检查它们的历史表现：

```

	#*****************************************************************
	# Overlay all Matches
	#****************************************************************** 		
	matches = matrix(NA, nr=(n.match+1), nc=3*n.query)
	temp = c(rep(NA, n.query), reference, query)
	for(i in 1:n.match) {
		matches[i,] = temp[ (min.index[i] - n.query + 1):(min.index[i] + 2*n.query) ]	
	}

	# add the 'query' pattern
	matches[(n.match+1),] = temp[ (len(temp) - 2*n.query + 1):(len(temp) + n.query) ]		

	# normalize
	for(i in 1:(n.match+1)) {
		matches[i,] = matches[i,] / matches[i,n.query]
	}

	#*****************************************************************
	# Plot all Matches
	#****************************************************************** 				
	temp = 100 * ( t(matches[,-c(1:n.query)]) - 1)

	par(mar=c(2, 4, 2, 2))
	matplot(temp, type='l',col='gray',lwd=2, lty='dotted', xlim=c(1,2.5*n.query),
		main = paste('Pattern Prediction with', n.match, 'neighbours'),ylab='Normalized', xlab='')
		lines(temp[,(n.match+1)], col='black',lwd=4)

	points(rep(2*n.query,n.match), temp[2*n.query,1:n.match], pch=21, lwd=2, col='gray', bg='gray')

	bt.plot.dot.label <- function(x, data, xfun, col='red') {
		for(j in 1:len(xfun)) {
			y = match.fun(xfun[[j]])(data)
			points(x, y, pch=21, lwd=4, col=col, bg=col)
			text(x, y, paste(names(xfun)[j], ':', round(y,1),'%'),
				adj=c(-0.1,0), cex = 0.8, col=col,xpd=TRUE)			
		}
	}

	bt.plot.dot.label(2*n.query, temp[2*n.query,1:n.match], 
		list(Min=min,Max=max,Median=median,'Bot 25%'=function(x) quantile(x,0.25),'Top 75%'=function(x) quantile(x,0.75)))
	bt.plot.dot.label(n.query, temp[n.query,(n.match+1)], list(Current=min))

```

![plot3.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/01/plot3-small1.png)

接下来，让我们用表格总结所有匹配项的表现：

```

	#*****************************************************************
	# Table with predictions
	#****************************************************************** 		
	temp = matrix( double(), nr=(n.match+4), 6)
		rownames(temp) = c(1:n.match, spl('Current,Min,Average,Max'))
		colnames(temp) = spl('Start,End,Return,Week,Month,Quarter')

	# compute returns
	temp[1:(n.match+1),'Return'] = matches[,2*n.query]/ matches[,n.query]
	temp[1:(n.match+1),'Week'] = matches[,(2*n.query+5)]/ matches[,2*n.query]
	temp[1:(n.match+1),'Month'] = matches[,(2*n.query+20)]/ matches[,2*n.query]
	temp[1:(n.match+1),'Quarter'] = matches[,(2*n.query+60)]/ matches[,2*n.query]

	# compute average returns
	index = spl('Return,Week,Month,Quarter')
	temp['Min', index] = apply(temp[1:(n.match+1),index],2,min,na.rm=T)
	temp['Average', index] = apply(temp[1:(n.match+1),index],2,mean,na.rm=T)
	temp['Max', index] = apply(temp[1:(n.match+1),index],2,max,na.rm=T)

	# format
	temp[] = plota.format(100*(temp-1),1,'','%')

	# enter dates
	temp['Current', 'Start'] = format(index(last(data,90)[1]), '%d %b %Y')
	temp['Current', 'End'] = format(index(last(data,1)[1]), '%d %b %Y')
	for(i in 1:n.match) {
		temp[i, 'Start'] = format(index(data[min.index[i] - n.query + 1]), '%d %b %Y')
		temp[i, 'End'] = format(index(data[min.index[i]]), '%d %b %Y')	
	}

	# plot table
	plot.table(temp, smain='Match #')

```

![plot4.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/01/plot4-small.png)

时间序列匹配分析可以用来猜测标普 500 在未来一周、一个月、一个季度的表现。这种猜测基于历史数据，历史上并没有保证会重复。

在下一篇文章中，我将检查时间序列匹配的其他距离度量，并展示一个[动态时间扭曲](http://en.wikipedia.org/wiki/Dynamic_time_warping)的示例。

要查看此例的完整源代码，请查看[github 上 bt.matching.test()函数的源代码](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
