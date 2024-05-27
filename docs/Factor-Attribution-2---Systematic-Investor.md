<!--yml

category: 未分类

date: 2024-05-18 14:39:55

-->

# 因子归因 2 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/06/27/factor-attribution-2/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/06/27/factor-attribution-2/#0001-01-01)

我想继续讨论我在[Factor Attribution](https://systematicinvestor.wordpress.com/2012/06/20/factor-attribution/)帖子中提出的因子归因主题。我已经重新组织了代码逻辑，分成以下 4 个函数：

+   factor.rolling.regression – 在给定滚动窗口上的因子归因

+   factor.rolling.regression.detail.plot – 每个因子的详细时间序列图和直方图

+   factor.rolling.regression.style.plot – 选定 2 个因子的历史风格图

+   factor.rolling.regression.bt.plot – 将基金表现与因子归因隐含的组合进行比较

让我们首先复制[Three Factor Rolling Regression Viewer](http://mas.xtreemhost.com/)网站上的风格和绩效图表，在[mas financial tools](http://mas.xtreemhost.com/)网站上。

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
	tickers = 'VISVX'

	periodicity = 'months'

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)
	for(i in ls(data)) {
		temp = adjustOHLC(data[[i]], use.Adjusted=T)							

		period.ends = endpoints(temp, periodicity)
			period.ends = period.ends[period.ends > 0]

		if(periodicity == 'months') {
			# reformat date to match Fama French Data
			monthly.dates = as.Date(paste(format(index(temp)[period.ends], '%Y%m'),'01',sep=''), '%Y%m%d')
			data[[i]] = make.xts(coredata(temp[period.ends,]), monthly.dates)
		} else
			data[[i]] = temp[period.ends,]
	}
	data.fund = data[[tickers]]

	#*****************************************************************
	# Fama/French factors
	#****************************************************************** 
	factors = get.fama.french.data('F-F_Research_Data_Factors', periodicity = periodicity,download = T, clean = F)

	# add factors and align
	data <- new.env()
		data[[tickers]] = data.fund
	data$factors = factors$data / 100
	bt.prep(data, align='remove.na', dates='1994::')

	#*****************************************************************
	# Facto Loadings Regression
	#****************************************************************** 
	obj = factor.rolling.regression(data, tickers, 36)

	#*****************************************************************
	# Reports
	#****************************************************************** 
	factor.rolling.regression.detail.plot(obj)

	factor.rolling.regression.style.plot(obj)

	factor.rolling.regression.bt.plot(obj)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/06/plot1-small2.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/06/plot2-small2.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/06/plot3-small1.png)

接下来，让我们再次添加来自[Kenneth R French: Data Library](http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html)的动量因子，并再次运行因子归因。

```

	#*****************************************************************
	# Fama/French factors + Momentum
	#****************************************************************** 
	factors = get.fama.french.data('F-F_Research_Data_Factors', periodicity = periodicity,download = T, clean = F)

	factors.extra = get.fama.french.data('F-F_Momentum_Factor', periodicity = periodicity,download = T, clean = F)	
		factors$data = merge(factors$data, factors.extra$data) 

	# add factors and align
	data <- new.env()
		data[[tickers]] = data.fund
	data$factors = factors$data / 100
	bt.prep(data, align='remove.na', dates='1994::')

	#*****************************************************************
	# Facto Loadings Regression
	#****************************************************************** 
	obj = factor.rolling.regression(data, tickers, 36)

	#*****************************************************************
	# Reports
	#****************************************************************** 
	factor.rolling.regression.detail.plot(obj)

	factor.rolling.regression.style.plot(obj)

	factor.rolling.regression.bt.plot(obj)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/06/plot4-small1.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/06/plot5-small1.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/06/plot7-small1.png)

为了从动量角度可视化风格，请创建一个显示基金在 HML / 动量空间中归因的风格图。

```

	factor.rolling.regression.style.plot(obj, xfactor='HML', yfactor='Mom')

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/06/plot6-small1.png)

我设计了因子归因函数，以接受任何用户指定的因子。这样，您就可以轻松地对来自[Kenneth R French: Data Library](http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html)的历史因子收益的任何组合运行因子归因，或者使用您自己的历史因子收益数据。

要查看此示例的完整源代码，请查看[github 上的 bt.test.r 中的 three.factor.rolling.regression()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
