<!--yml

类别：未分类

日期：2024-05-18 14:38:04

-->

# 将当前股票报价与历史价格合并 | 系统化投资者

> 来源：[`systematicinvestor.wordpress.com/2012/09/05/merging-current-stock-quotes-with-historical-prices/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/09/05/merging-current-stock-quotes-with-historical-prices/#0001-01-01)

上周我收到一个问题，是关于从回测转向实际交易的。例如，如果我们系统是基于今天的收盘价，我们可以通过下午 3:30 的价格来近似收盘价，确定信号并且还有时间进入交易。这并不完美，但是一种可能的解决方案。

不幸的是，在交易时段调用 getSymbols()函数只会返回前一个交易日的收盘价。以下是我今天在交易时段运行的示例：

```
	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')

	tickers = spl('VTI,EFA,SHY')	

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)							
	bt.prep(data)

	# look at the data
	last(data$prices, 2)

```

```
> last(data$prices, 2)
             EFA   SHY   VTI
2012-08-30 51.15 84.46 71.78
2012-08-31 51.60 84.51 72.21

```

没有 9 月 4 日的信息。

为了融入当前股票报价，我们需要将 getQuote()函数中的当前报价与 getSymbols()函数中的历史价格结合起来。以下是我今天在交易时段运行的示例：

```
	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')

	tickers = spl('VTI,EFA,SHY')	

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)							

		# current quotes logic
		quotes = getQuote(tickers)
		for(i in ls(data))
			if( last(index(data[[i]])) < as.Date(quotes[i, 'Trade Time']) ) {
				data[[i]] = rbind( data[[i]], make.xts(quotes[i, spl('Open,High,Low,Last,Volume,Last')],
					as.Date(quotes[i, 'Trade Time'])))
			}

	bt.prep(data)

	# look at the data
	last(data$prices, 2)

```

```
> last(data$prices, 2)
               EFA    SHY   VTI
2012-08-31 51.6000 84.510 72.21
2012-09-04 51.2561 84.495 71.87

```

当前的股票报价已经出现。我们可以在下午 3:30 左右运行我们的策略，确定信号并且还有时间进入交易。

要查看这个例子的完整源代码，请查看[github 上 bt.test.r 文件中的 bt.current.quote.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
