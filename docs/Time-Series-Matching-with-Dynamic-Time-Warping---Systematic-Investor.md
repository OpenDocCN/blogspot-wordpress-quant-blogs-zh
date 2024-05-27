<!--yml

分类：未分类

日期：2024-05-18 14:43:23

-->

# 动态时间规整的时间序列匹配 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/01/20/time-series-matching-with-dynamic-time-warping/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/01/20/time-series-matching-with-dynamic-time-warping/#0001-01-01)

这并非投资建议。本信息仅供参考。

在[时间序列匹配](https://systematicinvestor.wordpress.com/2012/01/13/time-series-matching/)文章中，我使用一对一映射来计算查询（当前模式）和参考（历史时间序列）之间的距离。以下图表可视化这个概念。距离是垂直线的总和。

![plot0.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/01/plot0-small.png)

将一个时间序列映射到另一个时间序列的另一种方法是[动态时间规整（DTW）](http://en.wikipedia.org/wiki/Dynamic_time_warping)。DTW 算法寻找查询和参考之间的最小距离映射。以下图表可视化 DTW 可能的 一对多映射。

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/01/plot1-small3.png)

为了检查简单的一对一映射和 DTW 之间是否有差异，我将搜索过去 10 年历史中与 SPY 最后 90 天相似的时间序列匹配。以下代码从雅虎财经加载历史价格，设置问题并使用[系统投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)计算历史滚动窗口的欧几里得距离：

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)
# https://systematicinvestor.wordpress.com/systematic-investor-toolbox/
###############################################################################
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')	
	tickers = 'SPY'

	data = getSymbols(tickers, src = 'yahoo', from = '1950-01-01', auto.assign = F)

	#*****************************************************************
	# Euclidean distance, one to one mapping
	#****************************************************************** 
	obj = bt.matching.find(Cl(data), normalize.fn = normalize.mean, dist.fn = 'dist.euclidean', plot=T)

	matches = bt.matching.overlay(obj, plot.index=1:90, plot=T)

	layout(1:2)
	matches = bt.matching.overlay(obj, plot=T, layout=T)
	bt.matching.overlay.table(obj, matches, plot=T, layout=T)

```

![plot2.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/01/plot2-small2.png)

![plot3.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/01/plot3-small2.png)

![plot4.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/01/plot4-small1.png)

接下来，让我们使用动态时间规整距离检查前 10 个匹配。我将使用[dtw](http://dtw.r-forge.r-project.org/)包中的动态时间规整实现。

```

	#*****************************************************************
	# Dynamic time warping distance	
	#****************************************************************** 
	# http://en.wikipedia.org/wiki/Dynamic_time_warping
	# http://dtw.r-forge.r-project.org/
	#****************************************************************** 
	load.packages('dtw')

	obj = bt.matching.find(Cl(data), normalize.fn = normalize.mean, dist.fn = 'dist.DTW', plot=T)

	matches = bt.matching.overlay(obj, plot.index=1:90, plot=T)

	layout(1:2)
	matches = bt.matching.overlay(obj, plot=T, layout=T)
	bt.matching.overlay.table(obj, matches, plot=T, layout=T)

```

![plot5.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/01/plot5-small.png)

![plot6.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/01/plot6-small.png)

![plot7.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/01/plot7-small.png)

这两种算法产生的匹配结果和预测结果非常相似。我会将这些预测作为对未来市场行为的合理猜测。到目前为止，市场在接下来的 22 天内似乎不会全力上涨。

要查看此例的完整源代码，请查看[bt.matching.dtw.test()函数在 github 上的 bt.test.r 文件](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
