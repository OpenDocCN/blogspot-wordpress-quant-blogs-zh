<!--yml

分类：未分类

日期：2024-05-18 14:43:11

-->

# 多因子模型——构建基本面因子 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/02/04/multiple-factor-model-building-fundamental-factors/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/02/04/multiple-factor-model-building-fundamental-factors/#0001-01-01)

这是关于多因子模型的系列文章中的第二篇。我将基于前一篇文章[《多因子模型——基本面数据》](https://systematicinvestor.wordpress.com/2012/01/29/multiple-factor-model-fundamental-data/)中展示的代码，展示如何构建 CSFB 阿尔法因子框架中描述的基本面因子。关于 CSFB 阿尔法因子框架的详细信息，请阅读[P. N. Patel, S. Yao, R. Carlson, A. Banerji, J. Handelman 的《CSFB 定量研究，阿尔法因子框架》第 11 页，第 49 页](http://www.scribd.com/mobile/documents/62210581/download?commit=Download+Now&secret_password=)。

CSFB 阿尔法因子框架既有传统的基本面因子，也有行业相对基本面因子。让我们先获取我们需要的用于创建市盈率、市销率、市现率、股息率、市净率因子的基本面数据。在前一篇文章中，我提到需要一段时间下载道琼斯指数中所有公司的历史基本面数据，并建议使用`save(data.fund, file='data.fund.Rdata')`命令保存基本面数据。在下面的代码中，我将使用`load(file='data.fund.Rdata')`命令加载历史基本面数据，而不是再次下载所有数据。

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)
# https://systematicinvestor.wordpress.com/systematic-investor-toolbox/
###############################################################################
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

	#*****************************************************************
	# Find Sectors for each company in DOW 30
	#****************************************************************** 
	tickers = spl('XLY,XLP,XLE,XLF,XLV,XLI,XLB,XLK,XLU')
	tickers.desc = spl('ConsumerCyclicals,ConsumerStaples,Energy,Financials,HealthCare,Industrials,Materials,Technology,Utilities')

	sector.map = c()
	for(i in 1:len(tickers)) {
		sector.map = rbind(sector.map, 
				cbind(sector.spdr.components(tickers[i]), tickers.desc[i])
			)
	}
	colnames(sector.map) = spl('ticker,sector')

	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')		
	tickers = dow.jones.components()

	sectors = factor(sector.map[ match(tickers, sector.map[,'ticker']), 'sector'])
		names(sectors) = tickers

	# get fundamental data
	load(file='data.fund.Rdata')

	# get pricing data
	load(file='data.Rdata')

	#*****************************************************************
	# Combine fundamental and pricing data
	#****************************************************************** 	
	for(i in tickers) {
		fund = data.fund[[i]]
		fund.date = date.fund.data(fund)

		# Earnings per Share		
		EPS = get.fund.data('Diluted EPS from Total Operations', fund, fund.date, is.12m.rolling=T)

		# Sales, exception not available for financial firms
		SALE = get.fund.data('total revenue', fund, fund.date, is.12m.rolling=T)

		# Common Shares Outstanding
		CSHO = get.fund.data('total common shares out', fund, fund.date)

		# Common Equity
		CEQ = get.fund.data('total equity', fund, fund.date)

		# Dividends
		DV.PS = get.fund.data('dividends paid per share', fund, fund.date, is.12m.rolling=T)

		# Cash Flow, exception not available for financial firms
		CFL = get.fund.data('net cash from operating activities', fund, fund.date, cash.flow=T, is.12m.rolling=T)

		# merge
		data[[i]] = merge(data[[i]], EPS, SALE, CSHO, CEQ, DV.PS, CFL)
	}

	bt.prep(data, align='keep.all', dates='1995::2011')

	#*****************************************************************
	# Create Factors
	#****************************************************************** 
	prices = data$prices
		prices = bt.apply.matrix(prices, function(x) ifna.prev(x))

	sectors	= sectors[colnames(prices)]	

	# create factors
	factors = list()	

```

在道琼斯指数中，有 4 家金融公司（AXP、BAC、JPM、TRV），对于金融公司来说，销售和现金流实际上是无法测量的。请阅读 A. Damodaran 的《估值金融服务业公司》一文，了解为什么对于金融公司来说，销售和现金流实际上是无法测量的。

接下来，让我们创建传统价值因子：市盈率、市销率、市现率、股息率、市净率。

```

	#*****************************************************************
	# Traditional Value
	#****************************************************************** 
	factors$TV = list()

	# Market Value - capitalization
	CSHO =  bt.apply(data, function(x) ifna.prev(x[, 'CSHO']))
	MKVAL = prices * CSHO

	# Price / Earnings
	EPS = bt.apply(data, function(x) ifna.prev(x[, 'EPS']))
	factors$TV$EP = EPS / prices

	# Price / Trailing Sales
	SALE = bt.apply(data, function(x) ifna.prev(x[, 'SALE']))	
	factors$TV$SP = SALE / MKVAL

	# Price / Trailing Cash Flow
	CFL = bt.apply(data, function(x) ifna.prev(x[, 'CFL']))
	factors$TV$CFP = CFL / MKVAL

	# Dividend Yield
	DV.PS = bt.apply(data, function(x) ifna.prev(x[, 'DV.PS']))
	factors$TV$DY = DV.PS / prices

	# Price / Book Value		
	CEQ = bt.apply(data, function(x) ifna.prev(x[, 'CEQ']))
	factors$TV$BP = CEQ	/ MKVAL

	# Eliminate Price/Sales and Price/Cash Flow for financial firms
	factors$TV$SP[, sectors == 'Financials'] = NA
	factors$TV$CFP[, sectors == 'Financials'] = NA

	#*****************************************************************
	# Convert to monthly
	#****************************************************************** 
	# find month ends
	month.ends = endpoints(prices, 'months')

	prices = prices[month.ends,]
		n = ncol(prices)
		nperiods = nrow(prices)

	ret = prices / mlag(prices) - 1
		next.month.ret = mlag(ret, -1)

	MKVAL = MKVAL[month.ends,]

	for(j in 1:len(factors)) {	
		for(i in 1:len(factors[[j]])) {
			factors[[j]][[i]] = factors[[j]][[i]][month.ends,]	
		}
	}

```

为了创建一个整体的传统价值因子，让我们首先标准化（转换为 z 分数）所有的传统价值因子，通过减去市值加权平均值并除以标准差。整体传统价值因子是所有标准化传统价值因子的平均值。

```

	#*****************************************************************
	# Create the overall Traditional Value factor 
	#****************************************************************** 
	# check missing data for financial firms
	sapply(factors$TV, count)	

	# normalize (convert to z scores) cross sectionaly all Traditional Value factors
	for(i in names(factors$TV)) {
		factors$TV[[i]] = (factors$TV[[i]] - cap.weighted.mean(factors$TV[[i]], MKVAL)) / 
							apply(factors$TV[[i]], 1, sd, na.rm=T)
	}

	# compute the overall Traditional Value factor
	load.packages('abind') 
	temp = abind(factors$TV, along = 3)
	factors$TV$AVG = factors$TV[[1]]
		factors$TV$AVG[] = apply(temp, c(1,2), mean, na.rm=T)

	# plot quintile charts for all Traditional Value factors
	layout(matrix(1:6,nc=2))
	sapply(1:len(factors$TV), function(i)
		compute.quantiles(factors$TV[[i]], next.month.ret, paste(names(factors$TV)[i], 'Traditional Value'))
	)

```

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/02/plot1-small.png)

我在[github 上的 factor.model.r 文件中创建了一个 compute.quantiles()函数](https://github.com/systematicinvestor/SIT/blob/master/R/factor.model.r)，用于计算和绘制分位数。例如，EP 因子的分位数图表显示了每个分位数中股票的平均下月表现。每个月通过 EP 因子对股票进行排名并将它们分为 5 个分位数。在大多数情况下，第五个分位数（Q5）的表现优于第一个分位数（Q1）。分位数之间的关系并不完美，但第五个分位数和第一个分位数之间的差距是正的。

接下来，让我们更详细地检查一下整体传统价值因子的分位数。

```

	#*****************************************************************
	# Backtest quantiles and quantile spread
	#****************************************************************** 
	out = compute.quantiles(factors$TV$AVG, next.month.ret, plot=F)	

	prices = data$prices
		prices = bt.apply.matrix(prices, function(x) ifna.prev(x))

	# create strategies that invest in each qutile
	models = list()

	for(i in 1:5) {
		data$weight[] = NA
			data$weight[month.ends,] = iif(out$quantiles == i, out$weights, 0)
			capital = 100000
			data$weight[] = (capital / prices) * (data$weight)	
		models[[paste('Q',i,sep='')]] = bt.run(data, type='share', capital=capital)
	}

	# spread
	data$weight[] = NA
		data$weight[month.ends,] = iif(out$quantiles == 5, out$weights, 
						iif(out$quantiles == 1, -out$weights, 0))
		capital = 100000
		data$weight[] = (capital / prices) * (data$weight)
	models$Q5_Q1 = bt.run(data, type='share', capital=capital)

	#*****************************************************************
	# Create Report
	#****************************************************************** 
	plotbt(models, plotX = T, log = 'y', LeftMargin = 3)	    	
		mtext('Cumulative Performance', side = 2, line = 1)

```

![plot2.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/02/plot2-small1.png)

第五个分位数和第一个分位数之间的差距（Q5-Q1）在 2000 年之后一直显示出一致的正表现，但在 1995 年到 2000 年之间是反向的。这有点奇怪，需要进一步调查。

在接下来的文章中，我将展示如何运行合并横截面回归来创建 alpha 分数。

要查看这个例子的完整源代码，请查看[github 上 factor.model.test.r 文件中的 fm.fund.factor.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/factor.model.test.r)。
