<!--yml

category: 未分类

date: 2024-05-18 14:34:33

-->

# 周末阅读 – S&P 500 可视化历史 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2013/01/20/weekend-reading-sp-500-visual-history/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/01/20/weekend-reading-sp-500-visual-history/#0001-01-01)

[主页](https://systematicinvestor.wordpress.com/ "转到主页")

[R](https://systematicinvestor.wordpress.com/category/r/)

> 周末阅读 – S&P 500 可视化历史

## 周末阅读 – S&P 500 可视化历史

Michael Johnston 在[ETF 数据库](http://etfdb.com/)与我分享了一个在假期期间与我分享的非常有趣的[帖子](http://etfdb.com/history-of-the-s-and-p-500/)。[S&P 500 可视化历史](http://etfdb.com/history-of-the-s-and-p-500/) – 是一个交互式帖子，展示了自 1980 年以来每年 S&P 500 中的前 10 个成分股。

另外，Judson Bishop 贡献了一个 plota.recession() 函数，用于向现有图表添加经济衰退条。经济衰退日期来自[美国经济研究局](http://www.nber.org/cycles.html)。以下是 plota.recession() 函数的一个简单示例。

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
	# Load historical data for ETFs
	#****************************************************************** 
	load.packages('quantmod')
	SPY = getSymbols('SPY', auto.assign = F)

	#*****************************************************************
	# Create Clusters
	#****************************************************************** 	
 	plota(SPY, type='l')
 		plota.recession()
 	plota.legend('SPY','black',SPY)

```

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2013/01/plot12.png)
