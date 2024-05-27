<!--yml

类别：未分类

日期：2024-05-18 14:39:18

-->

# Systematic Investor Toolbox 中的回测库介绍 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2011/11/25/introduction-to-backtesting-library-in-the-systematic-investor-toolbox/#0001-01-01`](https://systematicinvestor.wordpress.com/2011/11/25/introduction-to-backtesting-library-in-the-systematic-investor-toolbox/#0001-01-01)

我编写了一个简单的[回测](http://www.investopedia.com/terms/b/backtesting.asp)库来评估和分析交易策略。我将使用这个库来展示我将在接下来的系列帖子中研究的交易策略的表现。

在 R 中编写一个简单的回测程序非常容易，例如：

```

bt.simple <- function(data, signal) 
{
	# lag singal
	signal = Lag(signal, 1)

	# back fill
	signal = na.locf(signal, na.rm = FALSE)
	signal[is.na(signal)] = 0

	# calculate Close-to-Close returns
	ret = ROC(Cl(data), type='discrete')
	ret[1] = 0

	# compute stats	
	bt = list()
		bt$ret = ret * signal
		bt$equity = cumprod(1 + bt$ret)    	    	
	return(bt)
}

# Test for bt.simple functions
load.packages('quantmod')

# load historical prices from Yahoo Finance
data = getSymbols('SPY', src = 'yahoo', from = '1980-01-01', auto.assign = F)

# Buy & Hold
signal = rep(1, nrow(data))
buy.hold = bt.simple(data, signal)

# MA Cross
sma = SMA(Cl(data),200)
signal = ifelse(Cl(data) > sma, 1, 0)
sma.cross = bt.simple(data, signal)

# Create a chart showing the strategies perfromance in 2000:2009
dates = '2000::2009'
buy.hold.equity = buy.hold$equity[dates] / as.double(buy.hold$equity[dates][1])
sma.cross.equity = sma.cross$equity[dates] / as.double(sma.cross$equity[dates][1])

chartSeries(buy.hold.equity, TA = c(addTA(sma.cross.equity, on=1, col='red')),	
	theme ='white', yrange = range(buy.hold.equity, sma.cross.equity) )	

```

我在[Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)中实现的代码有点长，但遵循相同的逻辑。它提供了额外的功能：处理多个证券、权重或股份回测，以及自定义报告。以下是使用[Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)中的回测库实现上述策略的示例代码：

```

# Load Systematic Investor Toolbox (SIT)
setInternet2(TRUE)
con = gzcon(url('https://github.com/systematicinvestor/SIT/raw/master/sit.gz', 'rb'))
	source(con)
close(con)

	#*****************************************************************
	# Load historical data
	#****************************************************************** 	
	load.packages('quantmod')
	tickers = spl('SPY')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)
	bt.prep(data, align='keep.all', dates='1970::2011')

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 
	prices = data$prices    

	# Buy & Hold	
	data$weight[] = 1
	buy.hold = bt.run(data)	

	# MA Cross
	sma = bt.apply(data, function(x) { SMA(Cl(x), 200) } )	
	data$weight[] = NA
		data$weight[] = iif(prices >= sma, 1, 0)
	sma.cross = bt.run(data, trade.summary=T)			

	#*****************************************************************
	# Create Report
	#****************************************************************** 
	plotbt.custom.report(sma.cross, buy.hold)

```

**bt.prep** 函数合并并校准数据环境中的所有符号。**bt.apply** 函数将用户给定的函数应用于数据环境中的每个符号。**bt.run** 计算由 **data$weight** 矩阵指定的策略的权益曲线。**data$weight** 矩阵持有开仓/平仓的权重（信号）。**plotbt.custom.report** 函数创建自定义报告，用户可以对其进行微调。以下是样本输出：

```

> buy.hold = bt.run(data)
Performance summary :
        CAGR    Best    Worst
        7.2     14.5    -9.9

> sma.cross = bt.run(data, trade.summary=T)
Performance summary :
        CAGR    Best    Worst
        6.3     5.8     -7.2

```

视觉性能总结：

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot1-small8.png)

统计性能总结：

![plot2.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot2-small7.png)

交易总结：

![plot3.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot3-small5.png)

为了查看这个例子完整的源代码，请查看 github 上的 [bt.test() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.r)。
