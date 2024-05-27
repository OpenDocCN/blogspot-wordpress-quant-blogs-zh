<!--yml

类别：未分类

日期：2024-05-18 14:34:41

-->

# 最优聚类数 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2013/01/17/optimal-number-of-clusters/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/01/17/optimal-number-of-clusters/#0001-01-01)

在上一篇文章中，[当前主要市场聚类的例子](https://systematicinvestor.wordpress.com/2013/01/12/examples-of-current-major-market-clusters/)，我们根据 2012 年的相关性将主要市场聚类为 4 组。今天，我想继续讨论聚类主题，并讨论选择聚类数的方法。

我将探讨以下选择最优聚类数的方法：

+   至少解释 90%方差的最小聚类数

+   至少使每个聚类中所有组件之间的相关性为 40%的最小聚类数

+   [肘部方法](http://en.wikipedia.org/wiki/Determining_the_number_of_clusters_in_a_data_set)

首先让我们加载 10 大资产类的历史数据

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

	# get first 2 pricipal componenets
	xy = cmdscale(distance)

```

接下来，让我们从 2 个聚类迭代到 2/3N 个聚类（其中 N 是证券的数量），并在每次计算聚类解释的方差百分比和每个聚类中所有组件之间的最小相关性。

```

    #*****************************************************************
	# Determine number of clusters
	#****************************************************************** 
	n = ncol(data$prices)
		n1 = ceiling(n*2/3)

	# percentage of variance explained by clusters
	p.exp = rep(0,n1)

	# minimum correlation among all components in each cluster	
	min.cor = matrix(1,n1,n1)  

	for (i in 2:n1) {
		fit = kmeans(xy, centers=i, iter.max=100, nstart=100)
		p.exp[i] = 1- fit$tot.withinss / fit$totss

		for (j in 1:i) {
			index = fit$cluster == j
			min.cor[i,j] = min(correlation[index,index])
		}
	}

	# minimum number of clusters that explain at least 90% of variance
	min(which(p.exp > 0.9))

	# minimum number of clusters such that correlation among all components in each cluster is at least 40%
	# will not always work
	min(which(apply(min.cor[-1,],1,min,na.rm=T) > 0.4)) + 1

	# number of clusters based on elbow method
	find.maximum.distance.point(p.exp[-1]) + 1

```

在第一种方法中，我们将聚类数设置为解释至少 90%方差的最小聚类数。这不是一个坏选择；那么为什么是 90%，而不是 75%呢？

```

min(which(p.exp > 0.9))
[1] 4

```

在第二种方法中，我们将聚类数设置为使每个聚类中所有组件之间的相关性至少为 40%的最小聚类数。这也不是一个坏选择；那么为什么是 40%，而不是 50%呢？

```

min(which(apply(min.cor[-1,],1,min,na.rm=T) > 0.4)) + 1
[1] 5

```

在第三种方法中，我们使用[肘部方法](http://en.wikipedia.org/wiki/Determining_the_number_of_clusters_in_a_data_set)来设置聚类数。[肘部方法](http://en.wikipedia.org/wiki/Determining_the_number_of_clusters_in_a_data_set)背后的想法是观察添加每个额外聚类的边际收益。设置聚类数等于具有正边际收益的最大 K 值。从几何角度来看，如果你将聚类解释的方差百分比与聚类数绘制在图表上，曲线最远离 45 度线的点对应于最优聚类数。

```

find.maximum.distance.point(p.exp[-1]) + 1
[1] 4

```

所有方法都产生了类似的聚类数。让我们直观地看看 4 个和 5 个聚类之间的区别

```

	#*****************************************************************
	# Create Plot
	#****************************************************************** 	
	load.packages('cluster')
	fit = kmeans(xy, 4, iter.max=100, nstart=100)
	clusplot(xy, fit$cluster, color=TRUE, shade=TRUE, labels=3, lines=0, plotchar=F, 
		main = paste('Major Market Clusters over', dates, ', 4 Clusters'), sub='')

	fit = kmeans(xy, 5, iter.max=100, nstart=100)
	clusplot(xy, fit$cluster, color=TRUE, shade=TRUE, labels=3, lines=0, plotchar=F, 
		main = paste('Major Market Clusters over', dates, ', 5 Clusters'), sub='')

```

![plot2](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/01/plot2.png)

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/01/plot11.png)

这是一个判断问题，你觉得在这种情况下 4 个或 5 个聚类哪个更好？

我只是略微触及了表面，关于聚类的方法，你还可以使用资源来选择聚类的数量。我强烈建议关注关于聚类的背景和/或讨论：

在下一篇文章中，我将展示随着时间的推移集群的变化。之后，我将讨论[集群风险平价](http://cssanalytics.wordpress.com/)投资组合分配方法（Varadi，Kapler，2012 年）。关于[集群风险平价](http://cssanalytics.wordpress.com/)的更多详细信息，请阅读 David 在[`cssanalytics.wordpress.com/`](http://cssanalytics.wordpress.com/)的博客。

要查看此示例的完整源代码，请查看 github 上的[bt.cluster.optimal.number.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
