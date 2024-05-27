<!--yml

分类：未分类

日期：2024-05-18 14:44:20

-->

# 祝您 2022 年假期快乐，万事如意 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2011/12/23/happy-holidays-and-best-wishes-for-2012/#0001-01-01`](https://systematicinvestor.wordpress.com/2011/12/23/happy-holidays-and-best-wishes-for-2012/#0001-01-01)

这只是一张简短的便条，祝愿您和您的家人健康快乐，并度过美好的新年！希望您喜欢阅读我的博客，感谢您的评论和来信。

这是一个简短的 R 代码，实现了[Charting the Santa Claus Rally](http://ibankcoin.com/woodshedderblog/2011/12/15/charting-the-santa-claus-rally/)一文中 Woodshedder 的一个有趣的想法。我将绘制并比较本 12 月的 SPY 表现与以前 12 月的平均表现。

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
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)		
	bt.prep(data, align='remove.na', dates='1970::2011')

	#*****************************************************************
	# Prepare Data for the plot
	#****************************************************************** 
	prices = data$prices  
	n = len(tickers)  
	ret = prices / mlag(prices) - 1

	# find prices in December
	dates = index(prices)
	years = date.year(dates)	
	index = which(date.month(dates) == 12)

	# rearrange data in trading days
	trading.days = sapply(tapply(ret[index,], years[index], function(x) coredata(x)), function(x) x[1:22])

	# average return each trading days, excluding current year
	avg.trading.days = apply(trading.days[, -ncol(trading.days)], 1, mean, na.rm=T)
	current.year = trading.days[, ncol(trading.days)]

	# cumulative
	avg.trading.days = 100 * ( cumprod(1 + avg.trading.days) - 1 )
	current.year = 100 * ( cumprod(1 + current.year) - 1 )

	#*****************************************************************
	# Create Plot
	#****************************************************************** 	
	par(mar=c(4,4,1,1))
	plot(avg.trading.days, type='b', col=1,
		ylim=range(avg.trading.days,current.year,na.rm=T),
		xlab = 'Number of Trading Days in December',
		ylab = 'Avg % Profit/Loss'
		)
		lines(current.year, type='b', col=2)
	grid()
	plota.legend('Avg SPY,SPY Dec 2011', 1:2)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot1-small5.png)

希望今年不会让人失望，我们会看到年底的反弹。

如果想找到其他月份的平均表现，我建议阅读 CXO 咨询的[交易日历](http://www.cxoadvisory.com/trading-calendar/)文章。

要查看此示例的完整源代码，请查看 github 上的[bt.test.r 中的 bt.december.trading.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
