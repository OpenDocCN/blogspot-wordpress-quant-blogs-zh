<!--yml

类别：未分类

日期：2024-05-18 14:35:06

-->

# 选定主成分进行聚类 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/12/29/clustering-with-selected-principal-components/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/12/29/clustering-with-selected-principal-components/#0001-01-01)

在[可视化主成分](https://systematicinvestor.wordpress.com/2012/12/22/visualizing-principal-components/)文章中，我研究了 2012 年道琼斯工业平均指数中公司的[主成分](http://en.wikipedia.org/wiki/Principal_component_analysis)。今天，我想展示如何利用[主成分](http://en.wikipedia.org/wiki/Principal_component_analysis)创建[聚类](http://home.dei.polimi.it/matteucc/Clustering/tutorial_html/)（即根据彼此之间的距离形成相似公司的群组）。

让我们从加载我们在[可视化主成分](https://systematicinvestor.wordpress.com/2012/12/22/visualizing-principal-components/)文章中保存的道琼斯工业平均指数公司的历史价格开始。

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

	# load data saved in the bt.pca.test() function
	load(file='bt.pca.test.Rdata')

	#*****************************************************************
	# Principal component analysis (PCA), for interesting discussion
	# http://machine-master.blogspot.ca/2012/08/pca-or-polluting-your-clever-analysis.html
	#****************************************************************** 
	prices = data$prices	
	ret = prices / mlag(prices) - 1

	p = princomp(na.omit(ret))

	loadings = p$loadings[]

	x = loadings[,1]
	y = loadings[,2]
	z = loadings[,3]	

```

要创建[聚类](http://home.dei.polimi.it/matteucc/Clustering/tutorial_html/)，我将使用统计包中的层次聚类分析，hclust 函数。hclust 函数中的第一个参数是距离（不相似度）矩阵。为了计算距离矩阵，让我们取前 2 个主成分并计算每家公司之间的[欧氏距离](http://en.wikipedia.org/wiki/Euclidean_distance)：

```

	#*****************************************************************
	# Create clusters
	#****************************************************************** 		
	# create and plot clusters based on the first and second principal components
	hc = hclust(dist(cbind(x,y)), method = 'ward')
	plot(hc, axes=F,xlab='', ylab='',sub ='', main='Comp 1/2')
	rect.hclust(hc, k=3, border='red')

```

![plot1.png.small](https://systematicinvestor.wordpress.com/2012/12/29/clustering-with-selected-principal-components/plot1-png-small-69/)

同样，我们可以使用前三个主成分：

```

	# create and plot clusters based on the first, second, and third principal components
	hc = hclust(dist(cbind(x,y,z)), method = 'ward')
	plot(hc, axes=F,xlab='', ylab='',sub ='', main='Comp 1/2/3')
	rect.hclust(hc, k=3, border='red')

```

![plot2.png.small](https://systematicinvestor.wordpress.com/2012/12/29/clustering-with-selected-principal-components/plot2-png-small-66/)

另一个选择是使用[相关矩阵](http://en.wikipedia.org/wiki/Correlation_and_dependence)作为距离矩阵的代理：

```

	# create and plot clusters based on the correlation among companies
	hc = hclust(as.dist(1-cor(na.omit(ret))), method = 'ward')
	plot(hc, axes=F,xlab='', ylab='',sub ='', main='Correlation')
	rect.hclust(hc, k=3, border='red')

```

![plot3.png.small](https://systematicinvestor.wordpress.com/2012/12/29/clustering-with-selected-principal-components/plot3-png-small-46/)

请注意，[聚类](http://home.dei.polimi.it/matteucc/Clustering/tutorial_html/)将根据您使用的距离矩阵而有所不同。

要查看此示例的完整源代码，请查看[github 上的 bt.test.r 中的 bt.clustering.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
