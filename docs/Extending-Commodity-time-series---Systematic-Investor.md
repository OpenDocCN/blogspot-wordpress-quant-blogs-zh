<!--yml

类别：未分类

日期：2024 年 5 月 18 日 14:35:47

-->

# 延伸大宗商品时间序列 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/11/22/extending-commodity-time-series/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/11/22/extending-commodity-time-series/#0001-01-01)

我想跟进 [延伸黄金时间序列](https://systematicinvestor.wordpress.com/2012/09/11/extending-gold-time-series/) 帖子，展示我们如何延伸大宗商品时间序列。大多数大宗商品 ETF 于 2006 年开始交易，请参阅 [大宗商品 ETF 列表](http://etf.about.com/od/commodityetfs/a/List-Of-Commodity-Etfs.htm) 页面。我将使用 [DBC – PowerShares DB Commodity Fund](http://finance.yahoo.com/q?s=DBC)，作为大宗商品时间序列的代理。

不幸的是，[DBC – PowerShares DB Commodity Fund](http://finance.yahoo.com/q?s=DBC) 的基础指数的历史数据并不公开。因此，我将使用 [汤姆森路透/杰富瑞 CRB 指数](http://www.jefferies.com/cositemgr.pl/html/ProductsServices/SalesTrading/Commodities/ReutersJefferiesCRB/IndexData/index.shtml) 来延伸 [DBC – PowerShares DB Commodity Fund](http://finance.yahoo.com/q?s=DBC) 的时间序列。

我创建了一个辅助函数 [在 github 上的 data.r 中的 get.CRB() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/data.r)，用于下载和提取指数信息。请注意，我使用 gdata 包来读取指数数据，你可能需要本地 Perl 来使其正常工作。关于如何设置所有内容的很好的教程，请参阅 [如何使用 r 读取 excel 文件（dot xls 和 dot xlsx）到数据框中：gdata 和 perl](http://www.r-bloggers.com/how-to-read-an-excel-file-dot-xls-and-dot-xlsx-into-a-data-frame-with-r/) 帖子。

现在让我们将 CRB 指数和几个大宗商品 ETF 并排绘制，以直观检查它们的相似性：

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
	CRB = get.CRB()

	tickers = spl('GSG,DBC')		
	getSymbols(tickers, src = 'yahoo', from = '1970-01-01')

	#*****************************************************************
	# Compare different indexes
	#****************************************************************** 	
	out = na.omit(merge(Ad(CRB), Ad(GSG), Ad(DBC)))
		colnames(out) = spl('CRB,GSG,DBC')
	temp = out / t(repmat(as.vector(out[1,]),1,nrow(out)))

	# Plot side by side
	layout(1:2, heights=c(4,1))
	plota(temp, ylim=range(temp))
		plota.lines(temp[,1],col=1)
		plota.lines(temp[,2],col=2)
		plota.lines(temp[,3],col=3)
	plota.legend(colnames(temp),1:3)

	# Plot correlation table
	temp = compute.cor(temp / mlag(temp)- 1, 'pearson')
			temp[] = plota.format(100 * temp, 0, '', '%')
	plot.table(temp)	

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/11/plot1-small2.png)

CRB 指数的表现与大宗商品 ETF 相似；虽然不是完全复制，但鉴于缺乏公开的大宗商品指数历史数据，这已经足够。

接下来让我们将 DBC 的时间序列与 CRB 指数延伸，并将其用于一个简单的等权策略：

```

	#*****************************************************************
	# Create simple equal weight back-test
	#****************************************************************** 
	tickers = spl('GLD,DBC,TLT')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)

		# extend Gold and Commodity time series
		data$GLD = extend.GLD(data$GLD)	
		data$DBC = extend.data(data$DBC, get.CRB(), scale=T)

	bt.prep(data, align='remove.na')

	#*****************************************************************
	# Code Strategies
	#******************************************************************
	prices = data$prices      
	n = ncol(prices)

	# find period ends
	period.ends = endpoints(prices, 'months')
		period.ends = period.ends[period.ends > 0]

	models = list()

	#*****************************************************************
	# Equal Weight
	#******************************************************************
	data$weight[] = NA
		data$weight[period.ends,] = ntop(prices[period.ends,], n)   
	models$equal.weight = bt.run.share(data, clean.signal=F)

	#*****************************************************************
	# Create Report
	#******************************************************************       
	plotbt.custom.report.part1(models)       
	plotbt.custom.report.part2(models)       

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/11/plot2-small2.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/11/plot3-small1.png)

通过延伸 DBC 和 GLD 的时间序列，回测现在可以追溯到 2002 年 7 月，TLT 的首个交易日期。

要查看此示例的完整源代码，请查看 [github 上的 bt.test.r 中的 bt.extend.DBC.test() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
