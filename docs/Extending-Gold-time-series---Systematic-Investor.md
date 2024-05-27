<!--yml

category: 未分类

日期：2024-05-18 14:38:00

-->

# 扩展黄金时间序列 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/09/11/extending-gold-time-series/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/09/11/extending-gold-time-series/#0001-01-01)

在回测交易策略时，我希望所有资产都有很长的历史记录。不幸的是，有时没有具有足够历史记录的可交易股票或 ETF。例如，我可能将 [GLD](http://finance.yahoo.com/q?s=GLD) 用作黄金配置的代理，但是 [GLD](http://finance.yahoo.com/q?s=GLD) 只在 2004 年 11 月开始交易。

我们可以通过其基准指数 – 伦敦黄金午后定价 – 扩展 GLD 的历史收益。让我们首先从 [`www.kitco.com/gold.londonfix.html`](http://www.kitco.com/gold.londonfix.html) 下载并并排绘制 GLD 和伦敦黄金午后定价，方便的 CSV 下载由 [Wikiposit](http://wikiposit.org/w?filter=Finance/Commodities/) 提供。

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
	GLD = getSymbols('GLD', src = 'yahoo', from = '1970-01-01', auto.assign = F)			
		GLD = adjustOHLC(GLD, use.Adjusted=T)

	# get Gold.PM - London Gold afternoon fixing prices
	temp = read.csv('http://wikiposit.org/w?action=dl&dltypes=comma%20separated&sp=daily&uid=KITCO',skip=4,header=TRUE, stringsAsFactors=F)
	Gold.PM = make.xts(as.double(temp$Gold.PM) / 10, as.Date(temp$Date, '%d-%b-%Y'))
		Gold.PM = Gold.PM[ !is.na(Gold.PM), ]

	# merge GLD and Gold.PM
	data <- new.env()
		data$GLD = GLD
		data$Gold.PM = Gold.PM
	bt.prep(data, align='remove.na')

	#*****************************************************************
	# Plot GLD and Gold.PM
	#****************************************************************** 
	layout(1:2)
	plota(data$GLD, type='l', col='black', plotX=F)	
		plota.lines(data$Gold.PM, col='blue')	
	plota.legend('GLD,Gold.PM', 'black,blue', list(data$GLD, data$Gold.PM))

	# plot GLD and London afternoon gold fix spread
	spread = 100 * (Cl(data$GLD) - data$Gold.PM) / data$Gold.PM
	plota(spread , type='l', col='black')	
		plota.legend('GLD vs Gold.PM % spread', 'black', spread)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/09/plot1-small.png)

GLD 与其基准指数存在差异。请阅读 B. Zigler 的 [“黄金的‘纸质’价格”](http://www.hardassetsinvestor.com/interviews/2091-golds-paper-price.html) 文章，详细讨论和解释这种差异。

接下来，让我们使用其基准指数扩展 GLD 的时间序列（我创建了一个辅助函数 [github 上的 extend.GLD() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/data.r) 来简化该过程），并将其用于简单的等权重策略。

```

	#*****************************************************************
	# Create simple equal weight back-test
	#****************************************************************** 
	tickers = spl('GLD,TLT')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)

		# extend GLD with Gold.PM - London Gold afternoon fixing prices
		data$GLD = extend.GLD(data$GLD)

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

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/09/plot3-small.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/09/plot4-small.png)

通过扩展 GLD 的时间序列，回测现在可以追溯到 2002 年 6 月，TLT 的首个交易日期。

要查看此示例的完整源代码，请查看 [github 上的 bt.extend.GLD.test() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
