<!--yml

分类：未分类

date: 2024-05-18 14:35:14

-->

# 视觉化主成分 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/12/22/visualizing-principal-components/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/12/22/visualizing-principal-components/#0001-01-01)

[主成分分析（PCA）](http://en.wikipedia.org/wiki/Principal_component_analysis)是一种将观察值转换为称为主成分的线性不相关变量的过程([维基百科](http://en.wikipedia.org/wiki/Principal_component_analysis))。[PCA](http://en.wikipedia.org/wiki/Principal_component_analysis)是一种有用的描述工具，可帮助您检查数据。今天我将展示如何找到并可视化主成分。

让我们看看[道琼斯工业平均指数](http://en.wikipedia.org/wiki/Dow_Jones_Industrial_Average)在 2012 年的各成分。首先，我将下载[道琼斯工业平均指数](http://en.wikipedia.org/wiki/Dow_Jones_Industrial_Average)所有成分的历史价格和行业信息。

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
	# Find Sectors for each company in DOW 30
	#****************************************************************** 
	tickers = spl('XLY,XLP,XLE,XLF,XLV,XLI,XLB,XLK,XLU')
	tickers.desc = spl('ConsumerCyclicals,ConsumerStaples,Energy,Financials,HealthCare,Industrials,Materials,Technology,Utilities')

	sector.map = c()
	for(i in 1:len(tickers)) {
		sector.map = rbind(sector.map, 
				cbind(sector.spdr.components(tickers[i]), tickers.desc[i])
			)
	}
	colnames(sector.map) = spl('ticker,sector')

	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')	
	tickers = dow.jones.components()

	sectors = factor(sector.map[ match(tickers, sector.map[,'ticker']), 'sector'])
		names(sectors) = tickers

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '2000-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)	

	bt.prep(data, align='keep.all', dates='2012')

	# re-order sectors, because bt.prep can change the order of tickers
	sectors = sectors[data$symbolnames]

	# save data for later examples
	save(data, tickers, sectors, file='bt.pca.test.Rdata')

```

接下来，让我们对 2012 年各公司的回报运行[主成分分析（PCA）](http://en.wikipedia.org/wiki/Principal_component_analysis)并绘制每个主成分解释的方差百分比。

```

	#*****************************************************************
	# Principal component analysis (PCA), for interesting discussion
	# http://machine-master.blogspot.ca/2012/08/pca-or-polluting-your-clever-analysis.html
	#****************************************************************** 
	prices = data$prices	
	ret = prices / mlag(prices) - 1

	p = princomp(na.omit(ret))

	loadings = p$loadings[]
	p.variance.explained = p$sdev² / sum(p$sdev²)

	# plot percentage of variance explained for each principal component	
	barplot(100*p.variance.explained, las=2, xlab='', ylab='% Variance Explained')

```

![plot1.png.small](https://systematicinvestor.wordpress.com/2012/12/22/visualizing-principal-components/plot1-png-small-68/)

第一主成分，通常它是市场回报，在 2012 年解释了大约 45%的方差。

接下来，让我们绘制所有公司在第一和第二主成分上的载荷，并根据它们所属的行业突出显示点。

```

	#*****************************************************************
	# 2-D Plot
	#****************************************************************** 		
	x = loadings[,1]
	y = loadings[,2]
	z = loadings[,3]
	cols = as.double(sectors)

	# plot all companies loadings on the first and second principal components and highlight points according to the sector they belong
	plot(x, y, type='p', pch=20, col=cols, xlab='Comp.1', ylab='Comp.2')
	text(x, y, data$symbolnames, col=cols, cex=.8, pos=4)

	legend('topright', cex=.8,  legend = levels(sectors), fill = 1:nlevels(sectors), merge = F, bty = 'n') 

```

![plot2.png.small](https://systematicinvestor.wordpress.com/2012/12/22/visualizing-principal-components/plot2-png-small-65/)

请注意，同一行业的公司在图表上往往会聚在一起。

接下来，让我们再进一步，使用第一、第二和第三主成分创建一个 3D 图。

```

	#*****************************************************************
	# 3-D Plot, for good examples of 3D plots
	# http://statmethods.wordpress.com/2012/01/30/getting-fancy-with-3-d-scatterplots/
	#****************************************************************** 				
	load.packages('scatterplot3d') 

	# plot all companies loadings on the first, second, and third principal components and highlight points according to the sector they belong
	s3d = scatterplot3d(x, y, z, xlab='Comp.1', ylab='Comp.2', zlab='Comp.3', color=cols, pch = 20)

	s3d.coords = s3d$xyz.convert(x, y, z)
	text(s3d.coords$x, s3d.coords$y, labels=data$symbolnames, col=cols, cex=.8, pos=4)

	legend('topleft', cex=.8,  legend = levels(sectors), fill = 1:nlevels(sectors), merge = F, bty = 'n') 

```

![plot3.png.small](https://systematicinvestor.wordpress.com/2012/12/22/visualizing-principal-components/plot3-png-small-45/)

3D 图表确实增加了一些额外信息，但我发现 2D 图表更容易看。

在下一篇文章中，我将演示基于所选主成分的聚类，之后我想探索在[使用 PCA 进行价差交易](http://matlab-trading.blogspot.ca/2012/12/using-pca-for-spread-trading.html)一文中提出的有趣讨论。

假期快乐

要查看此例的完整源代码，请查看[bt.pca.test()函数在 github 上的 bt.test.r](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
