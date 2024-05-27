<!--yml

category: 未分类

date: 2024-05-18 14:34:57

-->

# 更多主成分乐趣 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2013/01/06/more-principal-components-fun/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/01/06/more-principal-components-fun/#0001-01-01)

今天，我想继续讨论[主成分](http://en.wikipedia.org/wiki/Principal_component_analysis)主题，并展示如何使用[主成分分析](http://en.wikipedia.org/wiki/Principal_component_analysis)构建与市场不相关的投资组合。 本文的大部分内容基于 Jev Kuznetsov 的出色文章[“Using PCA for spread trading”](http://matlab-trading.blogspot.ca/2012/12/using-pca-for-spread-trading.html)。

让我们从过去 5 年的[道琼斯工业平均指数](http://en.wikipedia.org/wiki/Dow_Jones_Industrial_Average)加载组件开始。

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
	tickers = dow.jones.components()

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '2009-01-01', env = data, auto.assign = T)
	bt.prep(data, align='remove.na')	

```

接下来，让我们基于价格历史的第一年计算[主成分](http://en.wikipedia.org/wiki/Principal_component_analysis)。

```

	#*****************************************************************
	# Principal component analysis (PCA), for interesting discussion
	# http://machine-master.blogspot.ca/2012/08/pca-or-polluting-your-clever-analysis.html
	#****************************************************************** 
	prices = last(data$prices, 1000)
		n = len(tickers)  		
	ret = prices / mlag(prices) - 1

	p = princomp(na.omit(ret[1:250,]))

	loadings = p$loadings[]

	# look at the first 4 principal components 	
	components = loadings[,1:4]

	# normalize all selected components to have total weight = 1
	components = components / repRow(colSums(abs(components)), len(tickers))

	# note that first component is market, and all components are orthogonal i.e. not correlated to market
	market = ret[1:250,] %*% rep(1/n,n)
	temp = cbind(market, ret[1:250,] %*% components)
		colnames(temp)[1] = 'Market'	

	round(cor(temp, use='complete.obs',method='pearson'),2)

	# the variance of each component is decreasing
	round(100*sd(temp,na.rm=T),2)

```

```

Correlation:
       Market Comp.1 Comp.2 Comp.3 Comp.4
Market    1.0      1    0.2    0.1      0
Comp.1    1.0      1    0.0    0.0      0
Comp.2    0.2      0    1.0    0.0      0
Comp.3    0.1      0    0.0    1.0      0
Comp.4    0.0      0    0.0    0.0      1

Standard Deviation:
Market Comp.1 Comp.2 Comp.3 Comp.4
   1.8    2.8    1.2    1.0    0.8

```

请注意，第一个主成分与市场高度相关，所有主成分之间的相关性都很低，与市场的相关性也很低。 此外，通过构建，主成分的波动性正在减小。 您可能想自己检查的一个有趣的观察：主成分在时间上相当持久（即，如果您使用未来价格计算相关性和波动性，例如，4 年的价格，主成分会保持其相关性和波动性概况）

接下来，让我们检查主成分中是否有任何均值回归。 我将使用增广迪基-富勒检验来检查主成分是否均值回归。（小的 p 值=>稳定，即均值回归）

```

	#*****************************************************************
	# Find stationary components, Augmented Dickey-Fuller test
	#****************************************************************** 	
	library(tseries)
	equity = bt.apply.matrix(1 + ifna(-ret %*% components,0), cumprod)
		equity = make.xts(equity, index(prices))

	# test for stationarity ( mean-reversion )
	adf.test(as.numeric(equity[,1]))$p.value
	adf.test(as.numeric(equity[,2]))$p.value
	adf.test(as.numeric(equity[,3]))$p.value
	adf.test(as.numeric(equity[,4]))$p.value

```

增广迪基-富勒检验表明第 4 个主成分是稳定的。 让我们更仔细地查看它的价格历史和组成：

```

	#*****************************************************************
	# Plot securities and components
	#*****************************************************************
	layout(1:2)

	# add Bollinger Bands
	i.comp = 4
	bbands1 = BBands(repCol(equity[,i.comp],3), n=200, sd=1)
	bbands2 = BBands(repCol(equity[,i.comp],3), n=200, sd=2)
	temp = cbind(equity[,i.comp], bbands1[,'up'], bbands1[,'dn'], bbands1[,'mavg'],
				bbands2[,'up'], bbands2[,'dn'])
		colnames(temp) = spl('Comp. 4,1SD Up,1SD Down,200 SMA,2SD Up,2SD Down')

	plota.matplot(temp, main=paste(i.comp, 'Principal component'))

	barplot.with.labels(sort(components[,i.comp]), 'weights')		

```

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/01/plot1-small.png)

价格历史以及 200 天移动平均线和 1、2 个布林带显示在顶部窗格上。 第 4 个主成分的投资组合权重显示在底部窗格上。

现在您拥有了一个均值回归的投资组合，同时也与市场不相关。 您可以以许多方式使用这些信息。 请分享您的想法和建议。

要查看此示例的完整源代码，请查看[github 上的 bt.test.r 中的 bt.pca.trading.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
