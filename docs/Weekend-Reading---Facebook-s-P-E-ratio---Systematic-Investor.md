<!--yml

类别：未分类

日期：2024-05-18 14:36:49

-->

# 周末阅读 – Facebook 的市盈率 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/10/07/weekend-reading-facebooks-pe-ratio/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/10/07/weekend-reading-facebooks-pe-ratio/#0001-01-01)

Barron's 文章 [Still Too Pricey by Andrew Bary](http://online.barrons.com/article/SB50001424053111904706204578002652028814658.html) 分析了 Facebook 的股价，并基于市盈率估值指标得出结论，即使在当前价格下，该股票也被高估了。我想展示如何使用[Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)进行这种基本分析。

首先让我们加载 Facebook 及科技部门的一些股票如 LinkedIn、Groupon、苹果和谷歌的历史价格和每股收益（EPS）。

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
	# Load historical fundamental and pricing data
	#****************************************************************** 
	load.packages('quantmod') 
	tickers = spl('FB,LNKD,GRPN,AAPL,GOOG')
	tickers.temp = spl('NASDAQ:FB,NYSE:LNKD,NASDAQ:GRPN,NASDAQ:AAPL,NASDAQ:GOOG')

	# get fundamental data
	data.fund <- new.env()
	for(i in 1:len(tickers)) {
			cat(tickers[i],'\n')
			data.fund[[tickers[i]]] = fund.data(tickers.temp[i], 80)
	}

	# get pricing data
	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)			

```

接下来，让我们结合基本和定价数据，并为所有股票创建市盈率。

```

	#*****************************************************************
	# Combine fundamental and pricing data
	#****************************************************************** 				
	for(i in tickers) {
		fund = data.fund[[i]]
		fund.date = date.fund.data(fund)

		# Earnings per Share		
		EPS = 4 * get.fund.data('Diluted EPS from Total Operations', fund, fund.date)
		if(nrow(EPS) > 3)
			EPS = rbind(EPS[1:3], get.fund.data('Diluted EPS from Total Operations', fund, fund.date, is.12m.rolling=T)[-c(1:3)])

		# merge	
		data[[i]] = merge(data[[i]], EPS)
	}

	bt.prep(data, align='keep.all', dates='1995::')

	#*****************************************************************
	# Create PE
	#****************************************************************** 
	prices = data$prices
		prices = bt.apply.matrix(prices, function(x) ifna.prev(x))

	EPS =  bt.apply(data, function(x) ifna.prev(x[, 'EPS']))

	PE = ifna(prices / EPS, NA)
		PE[ abs(EPS) < 0.001 ] = NA	

```

请注意，对于非常小的每股收益（EPS），市盈率会非常大；因此，在这种情况下，我将市盈率设为 NA。

困难的部分已经完成，现在让我们绘制所有公司的市盈率图表。

```

    #*****************************************************************
    # Create Report
    #******************************************************************       
    plota.matplot(PE)

    plota.matplot(PE, type='b',pch=20, dates='2012::')

    plota.matplot(EPS)

    plota.matplot(prices)

```

2012 年所有公司的市盈率：

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/10/plot1-small1.png)

2012 年所有公司的市盈率：

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/10/plot2-small1.png)

所有公司的每股收益（EPS）：

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/10/plot3-small.png)

所有公司的股价：

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/10/plot4-small.png)

从这些图表中我想说，仅基于历史市盈率基础判断 Facebook 是否被高估还为时过早，因为我们只有 3 份财务报表，还不足以做出明智的结论。你可能需要使用一年（FY1）和两年（FY2）的盈利预测来做出更好的决策。

这些图表中有趣的地方是 LinkedIn 如何维持其高得难以置信的市盈率？

我之前展示了如何获取和使用基本数据的示例。这里是供您参考的链接：

要查看此示例的完整源代码，请查看[github 上 fundamental.test.r 中的 fundamental.fb.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/fundamental.test.r)。
