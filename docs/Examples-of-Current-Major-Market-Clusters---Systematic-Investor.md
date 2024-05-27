<!--yml

类别：未分类

日期：2024-05-18 14:34:49

-->

# 当前主要市场群集示例 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2013/01/12/examples-of-current-major-market-clusters/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/01/12/examples-of-current-major-market-clusters/#0001-01-01)

我想跟进并提供一些关于 David Varadi 出色的[“当前主要市场群集的可视化”](http://cssanalytics.wordpress.com/2013/01/10/a-visual-of-current-major-market-clusters/)文章的更多细节。

让我们首先加载历史数据，了解 10 个主要资产类别：

+   黄金（[GLD](http://finance.yahoo.com/q?s=GLD)）

+   美元（[UUP](http://finance.yahoo.com/q?s=UUP)）

+   标普 500（[SPY](http://finance.yahoo.com/q?s=SPY)）

+   纳斯达克 100（[QQQ](http://finance.yahoo.com/q?s=QQQ)）

+   小盘股（[IWM](http://finance.yahoo.com/q?s=IWM)）

+   新兴市场（[EEM](http://finance.yahoo.com/q?s=EEM)）

+   国际股票（[EFA](http://finance.yahoo.com/q?s=EFA)）

+   房地产（[IYR](http://finance.yahoo.com/q?s=IYR)）

+   石油（[USO](http://finance.yahoo.com/q?s=USO)）

+   国债（[TLT](http://finance.yahoo.com/q?s=TLT)）

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
	load.packages('quantmod')

	tickers = spl('GLD,UUP,SPY,QQQ,IWM,EEM,EFA,IYR,USO,TLT')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1900-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)

	bt.prep(data, align='remove.na')

```

接下来，让我们使用过去一年的历史回报来计算所有资产类别之间的相关性，并将资产分组为 4 个群集：

```

	#*****************************************************************
	# Create Clusters
	#****************************************************************** 
	# compute returns
	ret = data$prices / mlag(data$prices) - 1
		ret = na.omit(ret)		

	# setup period and method to compute correlations
	dates = '2012::2012'
	method = 'pearson'	# kendall, spearman

	correlation = cor(ret[dates], method = method)    
        dissimilarity = 1 - (correlation)
        distance = as.dist(dissimilarity)

	# find 4 clusters      
	xy = cmdscale(distance)
	fit = kmeans(xy, 4, iter.max=100, nstart=100)

	#*****************************************************************
	# Create Plot
	#****************************************************************** 	
	load.packages('cluster')
	clusplot(xy, fit$cluster, color=TRUE, shade=TRUE, labels=3, lines=0, plotchar=F, 
		main = paste('Major Market Clusters over', dates), sub='')	

```

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/01/plot1.png)

有 4 个群集：TLT、GLD、UUP 和股票/石油/房地产。您可以执行以下命令查看分配的群集

```

	fit$cluster

```

这样做效果相当不错，但我们有许多事情要探讨：

+   如何选择群集数量

+   使用何种相关性度量，即皮尔逊、肯德尔、斯皮尔曼

+   选择回溯使用，即 1 个月/6 个月/1 年。

+   使用数据的频率，即日/周/月

在下一篇文章中，我将提供一些关于如何选择群集数量的想法。

要查看此示例的完整源代码，请查看[GitHub 上的 bt.test.r 中的 bt.cluster.visual.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
