<!--yml

category: 未分类

日期：2024-05-18 14:34:17

-->

# 季节性分析示例 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2013/02/04/an-example-of-seasonality-analysis/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/02/04/an-example-of-seasonality-analysis/#0001-01-01)

今天，我想演示创建季节性分析研究并生成样本摘要报告有多容易。作为示例研究，我将使用[Avondale Asset Management](http://www.avondaleam.com)发布的[S&P Annual Performance After a Big January](http://www.avondaleam.com/2013/02/s-annual-performance-after-big-january.html)帖子。

第一步是加载历史价格并找到大型一月事件。

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

	price = getSymbols('^GSPC', src = 'yahoo', from = '1900-01-01', auto.assign = F)

	# convert to monthly
	price = Cl(to.monthly(price, indexAt='endof'))				
	ret = price / mlag(price) - 1

	#*****************************************************************
	# Find Januaries with return > 4%
	#****************************************************************** 
	index =  which( date.month(index(ret)) == 1 & ret > 4/100 )

	# create summary table with return in January and return for the whole year
	temp = c(coredata(ret),rep(0,12))
	out = cbind(ret[index], sapply(index, function(i) prod(1 + temp[i:(i+11)])-1))
		colnames(out) = spl('January,Year')

```

所有的辛勤工作现在都已经完成，让我们创建一个图表和表格来总结[S&P Annual Performance After a Big January](http://www.avondaleam.com/2013/02/s-annual-performance-after-big-january.html)的数据。

```

	#*****************************************************************
	# Create Plot
	#****************************************************************** 
	col=col.add.alpha(spl('black,gray'),200)
	pos = barplot(100*out, border=NA, beside=T, axisnames = F, axes = FALSE,
		col=col, main='Annual Return When S&P500 Rises More than 4% in January')
		axis(1, at = colMeans(pos), labels = date.year(index(out)), las=2)
		axis(2, las=1)
	grid(NA, NULL)
	abline(h= 100*mean(out$Year), col='red', lwd=2)		
	plota.legend(spl('January,Annual,Average'),  c(col,'red'))

	# plot table
	plot.table(round(100*as.matrix(out),1))

```

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/02/plot1.png)

![plot2](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/02/plot21.png)

就是这样，我们做好了。

收获：创建季节性分析研究非常简单。接下来，您可能希望在一年中特定时间运行研究脚本，并在满足研究条件时发送提醒邮件。

要查看此示例的完整源代码，请查看[GitHub 上 bt.test.r 中的 bt.seasonality.january.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
