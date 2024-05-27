<!--yml

分类：未分类

日期：2024-05-18 14:34:25

-->

# 跟踪历史聚类数量 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2013/01/27/tracking-number-of-historical-clusters/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/01/27/tracking-number-of-historical-clusters/#0001-01-01)

在前一篇文章中，[最优聚类数量](https://systematicinvestor.wordpress.com/2013/01/17/optimal-number-of-clusters/)，我们探讨了选择聚类数量的方法。今天，我想继续聚类主题，并使用这些方法展示历史聚类数量时间序列。

特别是，我将查看以下选择最优聚类数量的方法：

+   解释至少 90%方差的最低聚类数

+   弯曲方法

+   层次聚类树在 1/3 高度处切割

首先，让我们加载 10 大资产类的历史价格。

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

然后，我创建了 3 个助手函数来自动选择聚类。特别是，我使用了以下选择最优聚类数量的方法：

+   解释至少 90%方差的最低聚类数 – cluster.group.kmeans.90 函数

+   弯曲方法 – cluster.group.kmeans.elbow 函数

+   层次聚类树在 1/3 高度处切割 – cluster.group.hclust 函数

要查看这些函数的完整源代码，请查看[github 上的 startegy.r](https://github.com/systematicinvestor/SIT/blob/master/R/strategy.r)。

让我们每周使用这些函数对数据集进行 250 天回溯来计算相关性。

```

	#*****************************************************************
	# Use following 3 methods to determine number of clusters
	# * Minimum number of clusters that explain at least 90% of variance
	#   cluster.group.kmeans.90
	# * Elbow method
	#   cluster.group.kmeans.elbow
	# * Hierarchical clustering tree cut at 1/3 height
	#   cluster.group.hclust
	#****************************************************************** 

	# helper function to compute portfolio allocation additional stats
	portfolio.allocation.custom.stats.clusters <- function(x,ia) {
		return(list(
			ncluster.90 = max(cluster.group.kmeans.90(ia)),
			ncluster.elbow = max(cluster.group.kmeans.elbow(ia)),
			ncluster.hclust = max(cluster.group.hclust(ia))
		))
	}

	#*****************************************************************
	# Compute # Clusters
	#****************************************************************** 		
	periodicity = 'weeks'
	lookback.len = 250

	obj = portfolio.allocation.helper(data$prices, 
		periodicity = periodicity, lookback.len = lookback.len,
		min.risk.fns = list(EW=equal.weight.portfolio),
		custom.stats.fn = portfolio.allocation.custom.stats.clusters
	) 

```

最后，每种方法的历史聚类数量时间序列图表：

```

	#*****************************************************************
	# Create Reports
	#****************************************************************** 		
	temp = list(ncluster.90 = 'Kmeans 90% variance',
		 ncluster.elbow = 'Kmeans Elbow',
		 ncluster.hclust = 'Hierarchical clustering at 1/3 height')	

	for(i in 1:len(temp)) {
		hist.cluster = obj[[ names(temp)[i] ]]
		title = temp[[ i ]]

		plota(hist.cluster, type='l', col='gray', main=title)
			plota.lines(SMA(hist.cluster,10), type='l', col='red',lwd=5)
		plota.legend('Number of Clusters,10 period moving average', 'gray,red', x = 'bottomleft')			
	}

```

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/01/plot1-small1.png)

![plot2.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/01/plot2-small.png)

![plot3.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/01/plot3-small.png)

所有方法选择的聚类略有不同，这是预期的。"解释至少 90%方差的最低聚类数"方法似乎产生了最稳定的结果。我建议查看更大的宇宙（例如 DOW30）和更长的时期（例如 1995 年至今）来评估这些方法。

要点：正如我在[最优聚类数量](https://systematicinvestor.wordpress.com/2013/01/17/optimal-number-of-clusters/)一文中提到的，创建聚类有多种不同的方法，而我只是略知一二。还有一个我尚未探索的维度——距离矩阵。目前，我使用相关矩阵作为距离度量来创建聚类。Matt Considine 指出，有一个 R 接口可以用于[最大信息基础非参数探索（MINE）](http://www.exploredata.net/)指标，该指标可以作为相关性的更好度量。

要查看此示例的完整源代码，请查看 github 上的 [bt.cluster.optimal.number.historical.test() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
