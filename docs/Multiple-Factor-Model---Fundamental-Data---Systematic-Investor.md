<!--yml

category: 未分类

date: 2024-05-18 14:42:48

-->

# 多因子模型 – 基本面数据 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/01/29/multiple-factor-model-fundamental-data/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/01/29/multiple-factor-model-fundamental-data/#0001-01-01)

[多因子模型](http://www.investopedia.com/terms/m/multifactor-model.asp) 可用于分解收益和计算风险。以下是多因子模型的一些示例：

模型中的因素通常使用定价、基本面、分析师估计和专有数据来创建。我只会展示使用定价和基本面数据的因素的示例，因为这些信息可以从 Yahoo Finance 和 ADVFN 轻松获取。

这是关于多因子模型系列的第一篇文章。在本文中，我将展示如何将公司的基本数据导入 R，创建一个简单的因子，并运行相关性分析。在接下来的文章中，我将展示如何：

+   构建因子并计算分位数差距

+   回测多因子模型

+   使用多因子模型计算风险

我在 github 的 fundamental.data.r 中创建了一个 [fund.data() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/fundamental.data.r)，用于从 ADVFN 下载公司的历史基本数据。以下代码加载了 [沃尔玛商店](http://www.google.com/finance?q=nyse:wmt) 的历史季度基本数据，并使用 [Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/) 计算了滚动年度 [每股收益 (EPS)](http://en.wikipedia.org/wiki/Earnings_per_share)：

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)
# https://systematicinvestor.wordpress.com/systematic-investor-toolbox/
###############################################################################
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

###############################################################################
# determine date when fundamental data is available
# use 'date preliminary data loaded' when available
# otherwise lag 'quarter end date' 2 months for Q1/2/3 and 3 months for Q4
###############################################################################		
date.fund.data <- function(data)
{
	# construct date
	quarter.end.date = as.Date(paste(data['quarter end date',], '/1', sep=''), '%Y/%m/%d')	
	quarterly.indicator = data['quarterly indicator',]
	date.preliminary.data.loaded = as.Date(data['date preliminary data loaded',], '%Y-%m-%d') + 1

	months = seq(quarter.end.date[1], tail(quarter.end.date,1)+365, by='1 month') 
	index = match(quarter.end.date, months)
	quarter.end.date = months[ iif(quarterly.indicator == '4', index+3, index+2) + 1 ] - 1

	fund.date = date.preliminary.data.loaded
		fund.date[is.na(fund.date)] = quarter.end.date[is.na(fund.date)] 

	return(fund.date)
}

	#*****************************************************************
	# Load historical fundamental data
	# http://advfn.com/p.php?pid=financials&symbol=NYSE:WMT&mode=quarterly_reports
	#****************************************************************** 
	Symbol = 'NYSE:WMT'	
	fund = fund.data(Symbol, 80)

	# construct date
	fund.date = date.fund.data(fund)	

	#*****************************************************************
	# Create and Plot Earnings per share
	#****************************************************************** 
	EPS.Q = as.double(fund['Diluted EPS from Total Operations',])
		EPS.Q = as.xts(EPS.Q, fund.date)	
	EPS = runSum(EPS.Q, 4)

	# Plot
	layout(1:2)
	par(mar=c(2,2,2,1))
	x = barplot(EPS.Q, main='Wal-Mart Quarterly Earnings per share', border=NA)
	text(x, EPS.Q, fund['quarterly indicator',], adj=c(0.5,-0.3), cex=0.8, xpd = TRUE)

	barplot(EPS, main='Wal-Mart Rolling Annual Earnings per share', border=NA)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/01/plot1-small4.png)

你可以看到沃尔玛的季度 EPS 存在明显的季节性，第四季度总是强劲且突出。处理损益表季节性的常见方法是使用滚动年度总和，即上一季度总和。

接下来，让我们对齐沃尔玛的价格和 EPS，并将它们绘制在同一张图上。

```

	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')
	tickers = 'WMT'

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)

	data$WMT = merge(data$WMT, EPS)
		# back fill EPS
		data$WMT$EPS = ifna.prev(coredata(data$WMT$EPS))	

	# Plot
	y = data$WMT['1990::']
	plota(Cl(y), type = 'l', LeftMargin=3)

	plota2Y(y$EPS, type='l', las=1, col='red', col.axis = 'red')

	plota.legend('WMT(rhs),WMT.EPS(lhs)', 'blue,red', list(Cl(y),y$EPS))

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/01/plot2-small3.png)

接下来，让我们为道琼斯指数中的所有公司重复上述步骤。

```

	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')		
	tickers = dow.jones.components()

	# get fundamental data
	data.fund <- new.env()
		temp = paste(iif( nchar(tickers) <= 3, 'NYSE:', 'NASDAQ:'), tickers, sep='')
		for(i in 1:len(tickers)) data.fund[[tickers[i]]] = fund.data(temp[i], 80)
	save(data.fund, file='data.fund.Rdata')

	# get pricing data
	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)	
	save(data, file='data.Rdata')

	#load(file='data.fund.Rdata')
	#load(file='data.Rdata')

	# combine fundamental and pricing data
	for(i in tickers) {
		fund = data.fund[[i]]
		fund.date = date.fund.data(fund)

		EPS.Q = as.double(fund['Diluted EPS from Total Operations',])
			EPS.Q = as.xts(EPS.Q, fund.date)	
		EPS = runSum(EPS.Q, 4)

		data[[i]] = merge(data[[i]], EPS)
	}

	bt.prep(data, align='keep.all', dates='1995::2011')

```

下载所有道琼斯指数公司的历史基本数据需要一些时间，所以我建议用 save(data.fund, file='data.fund.Rdata') 命令保存你的结果。稍后如果你想再次运行代码，只需加载(file='data.fund.Rdata')，而不是重新下载所有数据。

接下来，让我们创建月度因子。EP 因子 = (每股收益) / 价格。VOMO 因子 = 成交量 x 动量。

```

	#*****************************************************************
	# Compute monthly factors
	#****************************************************************** 
	prices = data$prices
		prices = bt.apply.matrix(prices, function(x) ifna.prev(x))

	# create factors
	factors = list()

	# E/P
	EPS = bt.apply(data, function(x) ifna.prev(x[, 'EPS']))
	factors$EP = EPS / prices

	# VOMO - Volume x Momentum
	volume = bt.apply(data, function(x) ifna.prev(Vo(x)))
	factors$VOMO = (prices / mlag(prices,10) - 1) * bt.apply.matrix(volume, runMean, 22) / bt.apply.matrix(volume, runMean, 66)

	# find month ends
	month.ends = endpoints(prices, 'months')

	prices = prices[month.ends,]
	n = ncol(prices)
	nperiods = nrow(prices)

	ret = prices / mlag(prices) - 1
	next.month.ret = mlag(ret, -1)

	factors$EP = factors$EP[month.ends,]	
	factors$VOMO = factors$VOMO[month.ends,]			

```

接下来，让我们对 EP 因子运行相关性分析。你可以将 VOMO 因子的相关性分析作为作业。

```

	#*****************************************************************
	# Correlation Analysis
	#****************************************************************** 
	x = as.vector(factors$EP)
 	y = as.vector(next.month.ret)

 	cor.test(x, y, use = 'complete.obs', method = 'pearson')			

 	# Plot
	par(mar=c(4,4,2,1)) 	 	 	
 	plot(x, y, pch=20, main='Correlation Analysis for EP factor', xlab='EP', ylab='Next Month Return')
 		abline(lm(y ~ x), col='blue', lwd=2)

```

![plot3.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/01/plot3-small3.png)

```

>  cor.test(x, y, use = 'complete.obs', method = 'pearson')
        Pearson's product-moment correlation
data:  x and y
t = 3.6931, df = 5867, p-value = 0.0002235
alternative hypothesis: true correlation is not equal to 0
95 percent confidence interval:
 0.02260247 0.07365350
sample estimates:
       cor
0.04815943

```

EP 与下月收益率之间的相关性很小，但与零有显著差异。这种小相关性并不令人惊讶，且在这种类型的分析中很常见。在接下来的文章中，我将展示即使这种微弱的相关性也可以是有利可图的。

要查看此例的完整源代码，请查看[github 上的 factor.model.test.r 文件中的 fm.fund.data.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/factor.model.test.r)。
