<!--yml

类别: 未分类

日期：2024-05-18 14:31:29

-->

# getSymbols Extra | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2013/11/26/getsymbols-extra/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/11/26/getsymbols-extra/#0001-01-01)

quantmod 包中的 [getSymbols](http://www.quantmod.com/documentation/getSymbols.html) 函数是将历史股价带入 R 环境的一种简单方便的方式。你需要指定股票代号列表、历史价格来源和日期。例如，以下命令将从雅虎财经下载‘RWX’、‘VNQ’、‘VGSIX’ 符号的历史股价：

```

	data <- new.env()
	getSymbols.extra(c('RWX','VNQ','VGSIX'), src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)

```

现在，**data** 环境包含了历史股价。例如，使用以下代码为 RWX 创建图表：

```

	plot(data$RWX)

```

有时，我发现 [getSymbols](http://www.quantmod.com/documentation/getSymbols.html) 功能可以扩展。例如，将系列重命名会很不错。即 RWX 是一只房地产 ETF，所以我们可以要求 [getSymbols](http://www.quantmod.com/documentation/getSymbols.html) 函数获取 RWX，但输出为 Real.Estate。另一个有用的功能是指定如何扩展数据的能力。即 RWX 只在 2007 年开始交易，将 RWX 时间序列方便地扩展为 VNQ 和 VGSIX。

我创建了 [getSymbols.extra](https://github.com/systematicinvestor/SIT/blob/master/R/utils.r) 函数来解决这些功能。[getSymbols.extra](https://github.com/systematicinvestor/SIT/blob/master/R/utils.r) 函数允许你以以下格式指定股票代号：

+   RWX：原始功能，即获取 RWX 的历史股价，可以通过 data$RWX 访问

+   Real.Estate = RWX：获取 RWX 的历史股价，将其重命名为 Real.Estate，并且可以通过 data$Real.Estate 访问

+   RWX + VNQ + VGSIX：获取 RWX、VNQ、VGSIX 的历史股价，将 RWX 与 VNQ 扩展，然后再用 VGSIX 扩展，可以通过 data$RWX 访问

+   Real.Estate = RWX + VNQ + VGSIX: 混合和匹配以上功能

让我们看一个例子：

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)
# https://systematicinvestor.wordpress.com/systematic-investor-toolbox/
###############################################################################
setInternet2(TRUE)
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

	tickers = spl('REIT=RWX, RWX+VNQ, REIT.LONG=RWX+VNQ+VGSIX')
	data <- new.env()
		getSymbols.extra(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)
	bt.start.dates(data)

	data$symbolnames = spl('REIT.LONG,RWX,REIT')
		for(i in data$symbolnames) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)
	bt.prep(data, align='keep.all') 	

	plota.matplot(data$prices)

```

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/11/plot1.png)

REIT.LONG 是使用 VNQ 扩展的 RWX，然后使用 VGSIX 扩展。

还有一种可能性，可以向 [getSymbols.extra](https://github.com/systematicinvestor/SIT/blob/master/R/utils.r) 函数提供自定义数据。即，那些不能通过 [getSymbols](http://www.quantmod.com/documentation/getSymbols.html) 函数获得的数据。

例如，为了扩展 GLD 时间序列，我们可能使用德国联邦银行的历史黄金价格。

```

	# Use extrenal data
	raw.data <- new.env()
		raw.data$GOLD = bundes.bank.data.gold()

	tickers = spl('GLD, GLD.LONG=GLD+GOLD')
	data <- new.env()
		getSymbols.extra(tickers, src = 'yahoo', from = '1980-01-01', env = data, raw.data = raw.data, auto.assign = T)
	bt.start.dates(data)
	data$symbolnames = spl('GLD.LONG,GLD')
   		for(i in data$symbolnames) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)
	bt.prep(data, align='keep.all') 	

	plota.matplot(data$prices)	

```

![plot2](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/11/plot2.png)

[getSymbols.extra](https://github.com/systematicinvestor/SIT/blob/master/R/utils.r)函数的主要目标是简化数据获取/准备步骤。如果遇到任何问题或有建议，请告诉我。

要查看此示例的完整源代码，请查看[github 上 utils.r 中的 getSymbols.extra.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/utils.r)。
