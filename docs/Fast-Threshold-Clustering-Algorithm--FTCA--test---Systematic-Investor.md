<!--yml

category: 未分类

日期：2024-05-18 14:31:20

-->

# Fast Threshold Clustering Algorithm (FTCA) test | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2013/11/28/fast-threshold-clustering-algorithm-ftca-test/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/11/28/fast-threshold-clustering-algorithm-ftca-test/#0001-01-01)

今天我想分享 [Fast Threshold Clustering Algorithm (FTCA)](http://cssanalytics.wordpress.com/2013/11/26/fast-threshold-clustering-algorithm-ftca/) 的测试和实现，该算法由 David Varadi 创建。此实现由 Pierre Chretien 开发并贡献，我只进行了小幅更新。

让我们首先复制 [Fast Threshold Clustering Algorithm (FTCA)](http://cssanalytics.wordpress.com/2013/11/26/fast-threshold-clustering-algorithm-ftca/) 文章中的结果：

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

	tickers = spl('XLY,XLP,XLE,XLF,XLV,XLI,XLB,XLK,XLU')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1900-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)		
	bt.prep(data, align='keep.all')

	#*****************************************************************
	# Helper function to compute portfolio allocation additional stats
	#****************************************************************** 
	portfolio.allocation.custom.stats.clusters <- function(x,ia) {
		return(list(
			clusters.FTCA = cluster.group.FTCA(0.5)(ia)			
		))
	}

	#*****************************************************************
	# Find clusters
	#****************************************************************** 		
	periodicity = 'months'
	lookback.len = 252

	obj = portfolio.allocation.helper(data$prices, 
		periodicity = periodicity, lookback.len = lookback.len,
		min.risk.fns = list(EW=equal.weight.portfolio),
		custom.stats.fn = portfolio.allocation.custom.stats.clusters
	) 			

	clusters = obj$clusters.FTCA$EW	
	clusters['2012:05::']

```

这些群集是稳定的，并且与 David 的结果相匹配

```

           XLB XLE XLF XLI XLK XLP XLU XLV XLY
2012-05-31   1   1   1   1   1   1   1   1   1
2012-06-29   1   1   1   1   1   1   1   1   1
2012-07-31   1   1   1   1   1   1   1   1   1
2012-08-31   1   1   1   1   1   1   1   1   1
2012-09-28   1   1   1   1   1   1   1   1   1
2012-10-31   1   1   1   1   1   1   1   1   1
2012-11-30   2   2   2   2   2   2   1   2   2
2012-12-31   2   2   2   2   2   2   1   2   2
2013-01-31   2   2   2   2   2   2   1   2   2
2013-02-28   1   1   1   1   1   1   1   1   1
2013-03-28   1   1   1   1   1   1   1   1   1
2013-04-30   1   1   1   1   1   1   1   1   1
2013-05-31   1   1   1   1   1   1   1   1   1
2013-06-28   1   1   1   1   1   1   1   1   1
2013-07-31   1   1   1   1   1   1   1   1   1
2013-08-30   1   1   1   1   1   1   1   1   1
2013-09-30   1   1   1   1   1   1   1   1   1
2013-10-31   1   1   1   1   1   1   1   1   1
2013-11-26   1   1   1   1   1   1   1   1   1

```

接下来我们比较使用 K-means 和 FTCA 的 Cluster Portfolio Allocation Algorithm：

```

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 					
	obj = portfolio.allocation.helper(data$prices, 
		periodicity = periodicity, lookback.len = lookback.len, 
		min.risk.fns = list(
			C.EW.kmeans = distribute.weights(equal.weight.portfolio, cluster.group.kmeans.90),
			C.EW.FTCA = distribute.weights(equal.weight.portfolio, cluster.group.FTCA(0.5))			
		)
	)

	models = create.strategies(obj, data)$models

	#*****************************************************************
	# Create Report
	#******************************************************************    
	barplot.with.labels(sapply(models, compute.turnover, data), 'Average Annual Portfolio Turnover')

```

两种聚类算法产生了非常相似的结果。一个显而易见的区别是周转率。由于 [Fast Threshold Clustering Algorithm (FTCA)](http://cssanalytics.wordpress.com/2013/11/26/fast-threshold-clustering-algorithm-ftca/) 产生了更稳定的群组，因此它的周转率较小。

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/11/plot11.png)

完整的源代码和示例可在 [strategy.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/strategy.r) 中找到 [cluster.group.FTCA() 函数的示例](https://github.com/systematicinvestor/SIT/blob/master/R/strategy.r)。
