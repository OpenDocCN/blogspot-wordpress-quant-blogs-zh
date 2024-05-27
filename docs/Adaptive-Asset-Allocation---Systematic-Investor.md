<!--yml

类别：未分类

日期：2024-05-18 14:38:22

-->

# 自适应资产配置 | 系统化投资者

> 来源：[`systematicinvestor.wordpress.com/2012/08/14/adaptive-asset-allocation/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/08/14/adaptive-asset-allocation/#0001-01-01)

今天我想强调一篇关于[巴特勒、菲尔布里克和戈迪洛提出的自适应资产配置论文](http://www.macquarieprivatewealth.ca/dafiles/Internet/mgl/ca/en/advice/specialist/darwin/documents/darwin-adaptive-asset-allocation.pdf)以及大卫·瓦拉迪关于[自适应资产配置算法参数的鲁棒性讨论](http://cssanalytics.wordpress.com/2012/07/17/adaptive-asset-allocation-combining-momentum-with-minimum-variance/)。

在这篇文章中，我将按照[自适应资产配置](http://www.macquarieprivatewealth.ca/dafiles/Internet/mgl/ca/en/advice/specialist/darwin/documents/darwin-adaptive-asset-allocation.pdf)论文的步骤进行，并在下一篇文章中展示如何测试自适应资产配置算法参数的敏感性。

我将使用与论文中提到的相同资产类别的 10 个 ETF：

+   美国股票（[SPY](http://www.google.com/finance?q=SPY)）

+   欧洲股票（[EFA](http://www.google.com/finance?q=EFA)）

+   日本股票（[EWJ](http://www.google.com/finance?q=EWJ)）

+   新兴市场股票（[EEM](http://www.google.com/finance?q=EEM)）

+   美国房地产投资信托基金（[IYR](http://www.google.com/finance?q=IYR)）

+   国际房地产投资信托基金（[RWX](http://www.google.com/finance?q=RWX)）

+   美国中期国债（[IEF](http://www.google.com/finance?q=IEF)）

+   美国长期国债（[TLT](http://www.google.com/finance?q=TLT)）

+   商品（[DBC](http://www.google.com/finance?q=DBC)）

+   黄金（[GLD](http://www.google.com/finance?q=GLD)）

不幸的是，这 10 个 ETF 中的大多数在 2004 年底才开始交易，因此我只能复制最近的自适应资产配置策略表现。

让我们从使用[系统化投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)加载 10 个 ETF 的历史价格开始：

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

	tickers = spl('SPY,EFA,EWJ,EEM,IYR,RWX,IEF,TLT,DBC,GLD')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)							
	bt.prep(data, align='keep.all', dates='2004:12::')

    #*****************************************************************
    # Code Strategies
    #******************************************************************
    prices = data$prices  
    n = ncol(prices)

    models = list()

    # find period ends
    period.ends = endpoints(prices, 'months')
        period.ends = period.ends[period.ends > 0]

	# Adaptive Asset Allocation parameters
	n.top = 5		# number of momentum positions
	n.mom = 6*22	# length of momentum look back
	n.vol = 1*22 	# length of volatility look back   

```

接下来，让我们按照白皮书中的指示创建投资组合：

```

    #*****************************************************************
    # Equal Weight
    #******************************************************************
    data$weight[] = NA
        data$weight[period.ends,] = ntop(prices[period.ends,], n)   
    models$equal.weight = bt.run.share(data, clean.signal=F)

    #*****************************************************************
    # Volatliliy Position Sizing
    #******************************************************************
    ret.log = bt.apply.matrix(prices, ROC, type='continuous')
    hist.vol = bt.apply.matrix(ret.log, runSD, n = n.vol)

    adj.vol = 1/hist.vol[period.ends,]

    data$weight[] = NA
        data$weight[period.ends,] = adj.vol / rowSums(adj.vol, na.rm=T)    
    models$volatility.weighted = bt.run.share(data, clean.signal=F)

    #*****************************************************************
    # Momentum Portfolio
    #*****************************************************************
    momentum = prices / mlag(prices, n.mom)

    data$weight[] = NA
        data$weight[period.ends,] = ntop(momentum[period.ends,], n.top)   
    models$momentum = bt.run.share(data, clean.signal=F)

    #*****************************************************************
    # Combo: weight positions in the Momentum Portfolio according to Volatliliy
    #*****************************************************************
    weight = ntop(momentum[period.ends,], n.top) * adj.vol

    data$weight[] = NA
        data$weight[period.ends,] = weight / rowSums(weight, na.rm=T)   
    models$combo = bt.run.share(data, clean.signal=F,trade.summary = TRUE)

```

最后让我们创建自适应资产配置投资组合：

```

    #*****************************************************************   
    # Adaptive Asset Allocation (AAA)
    # weight positions in the Momentum Portfolio according to 
    # the minimum variance algorithm
    #*****************************************************************   
    weight = NA * prices
        weight[period.ends,] = ntop(momentum[period.ends,], n.top)

    for( i in period.ends[period.ends >= n.mom] ) {
    	hist = ret.log[ (i - n.vol + 1):i, ]

		# require all assets to have full price history
		include.index = count(hist)== n.vol      

		# also only consider assets in the Momentum Portfolio
        index = ( weight[i,] > 0 ) & include.index
        n = sum(index)

		if(n > 0) {					
			hist = hist[ , index]

	        # create historical input assumptions
	        ia = create.historical.ia(hist, 252)
	            s0 = apply(coredata(hist),2,sd)       
	            ia$cov = cor(coredata(hist), use='complete.obs',method='pearson') * (s0 %*% t(s0))

			# create constraints: 0<=x<=1, sum(x) = 1
			constraints = new.constraints(n, lb = 0, ub = 1)
			constraints = add.constraints(rep(1, n), 1, type = '=', constraints)       

			# compute minimum variance weights				            
	        weight[i,] = 0        
	        weight[i,index] = min.risk.portfolio(ia, constraints)
        }
    }

    # Adaptive Asset Allocation (AAA)
    data$weight[] = NA
        data$weight[period.ends,] = weight[period.ends,]   
    models$aaa = bt.run.share(data, clean.signal=F,trade.summary = TRUE)

```

最后一步是为所有模型创建报告：

```

    #*****************************************************************
    # Create Report
    #******************************************************************    
    models = rev(models)

    plotbt.custom.report.part1(models)       
    plotbt.custom.report.part2(models)       
    plotbt.custom.report.part3(models$combo, trade.summary = TRUE)       
    plotbt.custom.report.part3(models$aaa, trade.summary = TRUE)       

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/08/plot1-small1.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/08/plot2-small1.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/08/plot3-small1.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/08/plot4-small1.png)

AAA 投资组合表现非常出色，产生了所有策略中最高的夏普比率和最小的回撤。在下一篇文章中，我将探讨 AAA 参数的敏感性。

要查看此示例的完整源代码，请查看[github 上的 bt.test.r 中的 bt.aaa.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
