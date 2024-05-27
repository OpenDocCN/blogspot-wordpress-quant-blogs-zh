<!--yml

类别：未分类

日期：2024-05-18 14:29:45

-->

# 调整后的动量 | 系统化投资者

> 来源：[`systematicinvestor.wordpress.com/2014/08/01/adjusted-momentum/#0001-01-01`](https://systematicinvestor.wordpress.com/2014/08/01/adjusted-momentum/#0001-01-01)

## 调整后的动量

David Varadi 发表了两篇关于动量烹饪的优秀帖子/想法：

我忍不住想与你分享这些想法。以下是使用[系统化投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)的实现。

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

	tickers = spl('SPY,^VIX')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)
		for(i in data$symbolnames) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)
	bt.prep(data, align='remove.na', fill.gaps = T)

	VIX = Cl(data$VIX)
	bt.prep.remove.symbols(data, 'VIX')

	#*****************************************************************
	# Setup
	#*****************************************************************
	prices = data$prices

	models = list()

	#*****************************************************************
	# 200 SMA
	#****************************************************************** 
	data$weight[] = NA
		data$weight[] = iif(prices > SMA(prices, 200), 1, 0)
	models$ma200 = bt.run.share(data, clean.signal=T)

	#*****************************************************************
	# 200 ROC
	#****************************************************************** 
	roc = prices / mlag(prices) - 1

	data$weight[] = NA
		data$weight[] = iif(SMA(roc, 200) > 0, 1, 0)
	models$roc200 = bt.run.share(data, clean.signal=T)

	#*****************************************************************
	# 200 VIX MOM
	#****************************************************************** 
	data$weight[] = NA
		data$weight[] = iif(SMA(roc/VIX, 200) > 0, 1, 0)
	models$vix.mom = bt.run.share(data, clean.signal=T)

	#*****************************************************************
	# 200 ER MOM
	#****************************************************************** 
	forecast = SMA(roc,10)
	error = roc - mlag(forecast)
	mae = SMA(abs(error), 10)

	data$weight[] = NA
		data$weight[] = iif(SMA(roc/mae, 200) > 0, 1, 0)
	models$er.mom = bt.run.share(data, clean.signal=T)

	#*****************************************************************
	# Report
	#****************************************************************** 
	strategy.performance.snapshoot(models, T)

```

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/08/plot1.png)

**请享受并与 David 和我分享您的想法。**

要查看此示例的完整源代码，请查看

[bt.adjusted.momentum.test() 函数在 github 的 bt.test.r 中](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r).
