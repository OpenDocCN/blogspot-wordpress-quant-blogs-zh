<!--yml

分类：未分类

日期：2024 年 05 月 18 日 14:36:33

-->

# 使用折现现金流量进行公司估值 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/10/19/company-valuation-using-discounted-cash-flows/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/10/19/company-valuation-using-discounted-cash-flows/#0001-01-01)

今天我想展示一个简单的例子，说明我们如何使用[折现现金流量（DCF）分析](http://en.wikipedia.org/wiki/Discounted_cash_flow)对公司进行估值。其想法是根据折现的未来现金流来计算公司的内在价值。为了计算未来的现金流，我将使用历史自由现金流的增长率。为了计算这些现金流的现值，我将使用保守的 9%折现率。如果您想了解更多关于[折现现金流量（DCF）分析](http://en.wikipedia.org/wiki/Discounted_cash_flow)的信息，我建议您参考以下参考资料：

首先，让我们使用[系统投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)加载苹果（AAPL）的历史价格和基本数据。

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
	tickers = spl('AAPL')
	tickers.temp = spl('NASDAQ:AAPL')

	# get fundamental data
	data.fund <- new.env()
	for(i in 1:len(tickers))
		data.fund[[tickers[i]]] = fund.data(tickers.temp[i], 80, 'annual')

	# get pricing data
	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)			

	# prepare data
	fund = data.fund[[tickers[1]]]
	fund.date = date.fund.data(fund)			
	price = Cl(data[[tickers[1]]]['1995::'])

```

接下来，让我们提取[折现现金流量（DCF）分析](http://en.wikipedia.org/wiki/Discounted_cash_flow)的基本数据。

```

	#*****************************************************************
	# Extract Inputs for DCF Valuation
	#****************************************************************** 				
	# Free Cash Flows
	FCF = get.fund.data('free cash flow', fund, fund.date)

	# Invested Capital
	IC = get.fund.data('invested capital', fund, fund.date)

	# Sales
	SALE = get.fund.data('total revenue', fund, fund.date)

	# Common Equity
	CEQ = get.fund.data('total equity', fund, fund.date)

	# Common Shares Outstanding
	CSHO = get.fund.data('total common shares out', fund, fund.date)

	# Growth Rate
	CROIC = FCF/IC

	# Average inputs
	g = runMean(CROIC, 5)
	cash = runMean(FCF, 5)

```

接下来，我创建了一个简单的函数来估算公司的内在价值，使用[折现现金流量（DCF）分析](http://en.wikipedia.org/wiki/Discounted_cash_flow)。

```

	#*****************************************************************
	# Helper function to compute Intrinsic Value
	#****************************************************************** 				
	compute.DCF.IV <- function(cash, eqity, shares, g, R) {
		if( cash <= 0 ) return(NA)

		if( len(R) == 1 ) R = rep(R, len(g))

		value = eqity + sum(cash * cumprod(1 + g) / cumprod(1 + R))
		return( value / shares )
	}

```

最后，让我们计算 AAPL 的内在价值并创建图表。

```

	#*****************************************************************
	# Compute Intrinsic Value, assumptions:
	# Company will grow for the first 3 years at current Growth Rate
	# slowed down by 20% for the next 4 years, and slowed down by a further 20% for the next 3 years
	# and finally 3% growth for the next 10 years
	#
	# The Discount Rate is 9%
	#
	# http://www.oldschoolvalue.com/blog/stock-analysis/apple-aapl-valuation/
	#****************************************************************** 				
	dcf.price = NA * g
	i.start = which(!is.na(g))[1] 

	for(i in i.start : nrow(g)) {
		# Create Growth Rate scenario: 		
		g.scenario = c(rep(g[i],3), rep(g[i],4)*0.8, rep(g[i],3)*0.8*0.8, rep(3/100,10))

		# Compute Intrinsic Value
		dcf.price[i] = compute.DCF.IV(cash[i], CEQ[i], CSHO[i], g.scenario, 9/100)
	}

	#*****************************************************************
	# Create Plots
	#****************************************************************** 
	plota(price, type='l', log = 'y', col='blue', main=tickers[1],
		ylim=range(price,dcf.price,na.rm=T))
	plota.lines(dcf.price, type='s', col='red', lwd=2)
	plota.legend('Close,Intrinsic Value', 'blue,red', list(price, dcf.price))	

	plota(g, type='b', col='blue', pch=0, main='Growth Rate')	

	plota(cash, type='b', col='blue', pch=0, main='Free Cash Flows')	

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/10/plot1.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/10/plot2.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/10/plot3.png)

对于您在[折现现金流量（DCF）分析](http://en.wikipedia.org/wiki/Discounted_cash_flow)中使用的公司增长率和折现率的假设，内在价值的计算非常敏感。

在过去的 5 年中，AAPL 经历了惊人的增长率，而重要的问题是 AAPL 是否能够在未来保持这种增长率。如果是的话，那么根据[折现现金流量（DCF）分析](http://en.wikipedia.org/wiki/Discounted_cash_flow)的建议，股价很容易达到新的高点。

要查看此示例的完整源代码，请查看[github 上 fundamental.test.r 中的 fundamental.dcf.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/fundamental.test.r)。
