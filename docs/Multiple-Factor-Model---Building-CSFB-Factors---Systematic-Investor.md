<!--yml

category: 未分类

date: 2024-05-18 14:42:58

-->

# 构建 CSFB 因子 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/02/13/multiple-factor-model-building-csfb-factors/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/02/13/multiple-factor-model-building-csfb-factors/#0001-01-01)

这是关于多因子模型的系列中的第三篇文章。我将在之前的帖子中介绍的代码基础上进行讲解，[多因子模型 - 构建基本因子](https://systematicinvestor.wordpress.com/2012/02/04/multiple-factor-model-building-fundamental-factors/)，并展示如何构建 CSFB Alpha 因子框架中描述的大多数因子。有关 CSFB Alpha 因子框架的详细信息，请阅读[CSFB 定量研究，Alpha 因子框架第 11 页，第 49 页，作者为 P. N. Patel、S. Yao、R. Carlson、A. Banerji、J. Handelman](http://www.scribd.com/mobile/documents/62210581/download?commit=Download+Now&secret_password=)。

本文将包括长篇代码以提取/格式化数据和构建因子。我在[github 上的 factor.model.r](https://github.com/systematicinvestor/SIT/blob/master/R/factor.model.r)创建了一些数据操作和可视化的辅助函数。例如，consecutive.changes 函数计算连续正变化的数量。

本文的大纲：

+   创建大部分 CSFB 因子

+   创建并测试复合平均因子

+   运行横截面回归以估计因子载荷

+   创建并测试使用估计因子载荷的 Alpha 模型

让我们从获取基本数据并创建因子开始。在之前的帖子中，我提到下载道琼斯指数中所有公司的历史基本数据需要一段时间，我建议使用`save(data.fund, file=’data.fund.Rdata’)`命令保存基本数据。在以下代码中，我将使用`load(file=’data.fund.Rdata’)`命令加载历史基本数据，而不是再次下载所有数据。

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
	load.packages('quantmod,abind')		
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
			nperiods = ncol(fund)

		# D - holds all data to be merged with pricing data
		D = list()

		#--------------------------------------------------------------
		# Data for Traditional and Relative Value	
		#--------------------------------------------------------------

		# Earnings per Share		
		D$EPS = get.fund.data('Diluted EPS from Total Operations', fund, fund.date, is.12m.rolling=T)

		# Sales, exception not available for financial service firms
		D$SALE = get.fund.data('total revenue', fund, fund.date, is.12m.rolling=T)

		# Common Shares Outstanding
		D$CSHO = get.fund.data('total common shares out', fund, fund.date)

		# Common Equity
		D$CEQ = get.fund.data('total equity', fund, fund.date)

		# Dividends
		D$DV.PS = get.fund.data('dividends paid per share', fund, fund.date, is.12m.rolling=T)

		# Cash Flow
		D$CFL = get.fund.data('net cash from operating activities', fund, fund.date, cash.flow=T, is.12m.rolling=T)

		#--------------------------------------------------------------
		# Data for Historical Growth	
		#--------------------------------------------------------------

		# Consecutive Quarters of Positive Changes in Trailing 12 Month Cash Flow
		D$CFL.CON.CHG = consecutive.changes(D$CFL)		
			# check
			#merge(D$CFL, sign(diff(D$CFL)), consecutive.changes(D$CFL), consecutive.changes(D$CFL,F))

		# Consecutive Quarters of Positive Change in Quarterly Earnings
		D$EPS.CON.CHG = consecutive.changes(D$EPS)

		# 12 Month Change in Quarterly Cash Flow
		temp = get.fund.data('net cash from operating activities', fund, fund.date, cash.flow=T)
		D$CFL.CHG = temp / mlag(temp,4)

		# 3 Year Average Annual Sales Growth
		D$SALE.3YR.GR = D$SALE
		if(!all(is.na(D$SALE))) D$SALE.3YR.GR = SMA(ifna(D$SALE / mlag(D$SALE,4) - 1,NA), 3*4)

		# 3 Year Average Annual Earnings Growth
		D$EPS.3YR.GR = SMA(D$EPS / mlag(D$EPS,4) - 1, 3*4)

		# 12 Quarter Trendline in Trailing 12 Month Earnings		
		D$EPS.TREND = D$EPS * NA
			D$EPS.TREND[12:nperiods] = sapply(12:nperiods, function(i) beta.degree(ols(cbind(1,1:12), D$EPS[(i-12+1):i])$coefficients[2]))

		# Slope of Trend Line Through Last 4 Quarters of Trailing 12M Cash Flows		
		D$CFL.TREND = D$CFL * NA
			D$CFL.TREND[4:nperiods] = sapply(4:nperiods, function(i) beta.degree(ols(cbind(1,1:4), D$CFL[(i-4+1):i])$coefficients[2]))

		#--------------------------------------------------------------
		# Data for Profit Trends	
		#--------------------------------------------------------------
		RECT = get.fund.data('receivables', fund, fund.date)
		INVT = get.fund.data('inventories', fund, fund.date)

		D$AT = get.fund.data('total assets', fund, fund.date)
		XSGA = get.fund.data('Selling, General & Administrative (SG&A) Expense', fund, fund.date, is.12m.rolling=T)

		# Consecutive Quarters of Declines in (Receivables+Inventories) / Sales
		D$RS.CON.CHG = consecutive.changes((RECT + INVT) / D$SALE, F)

		# Consecutive Qtrs of Positive Change in Trailing 12M Cash Flow / Sales
		D$CS.CON.CHG = consecutive.changes(D$CFL/D$SALE)

		# Overhead = sales, general and administrative costs
		# Consecutive Quarters of Declines in Trailing 12 Month Overhead / Sales
		D$OS.CON.CHG = consecutive.changes(XSGA/D$SALE, F)

		# (Industry Relative) Trailing 12 Month (Receivables+Inventories) / Sales
		D$RS = (RECT + INVT) / D$SALE

		# (Industry Relative) Trailing 12 Month Sales / Assets
		D$SA = D$SALE / D$AT

		# Trailing 12 Month Overhead / Sales
		D$OS = XSGA / D$SALE

		# Trailing 12 Month Earnings / Sales
		D$ES = D$EPS / D$SALE						

		#--------------------------------------------------------------
		# Merge Fundamental and Pricing data
		#--------------------------------------------------------------

		# merge	
		data[[i]] = merge(data[[i]], as.xts(abind(D,along=2), fund.date))						
	}

	bt.prep(data, align='keep.all', dates='1995::2011')

	#*****************************************************************
	# Create Factors
	#****************************************************************** 
	prices = data$prices	
		prices = bt.apply.matrix(prices, function(x) ifna.prev(x))

	# re-map sectors
	sectors	= sectors[colnames(prices)]	

	# create factors
	factors = list()
	factor.names = list()	

```

接下来让我们创建大部分 CSFB 因子。

```

	#*****************************************************************
	# Create Traditional Value
	#****************************************************************** 
	factors$TV = list()
	factor.names$TV = 'Traditional Value'

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
	# Create Historical Growth
	#****************************************************************** 
	factors$HG = list()
	factor.names$HG = 'Historical Growth'

	for(i in spl('CFL.CON.CHG,EPS.CON.CHG,CFL.CHG,SALE.3YR.GR,EPS.3YR.GR,EPS.TREND,CFL.TREND')) {
		factors$HG[[i]] = bt.apply(data, function(x) ifna.prev(x[, i]))
	}

	#*****************************************************************
	# Create Profit Trends
	#****************************************************************** 
	factors$PT = list()		
	factor.names$PT = 'Profit Trends'	

	for(i in spl('RS.CON.CHG,CS.CON.CHG,OS.CON.CHG,RS,SA,OS,ES')) {
		factors$PT[[i]] = bt.apply(data, function(x) ifna.prev(x[, i]))
	}

	#*****************************************************************
	# Create Price Momentum
	#****************************************************************** 
	factors$PM = list()
	factor.names$PM = 'Price Momentum'	

	# find week ends
	week.ends = endpoints(prices, 'weeks')
		week.prices = prices[week.ends,]
		week.nperiods = nrow(week.prices)

	#Slope of 52 Week Trend Line
	factors$PM$S52W.TREND = bt.apply.matrix(week.prices, function(x) {
		c(rep(NA,51),
		sapply(52:week.nperiods, function(i) beta.degree(ols(cbind(1,1:52), x[(i - 52 + 1):i])$coefficients[2]))
		)})

	#4/52 Week Price Oscillator
	factors$PM$PP04.52W = bt.apply.matrix(week.prices, EMA, 4) / bt.apply.matrix(week.prices, EMA, 52)

	#39 Week Return
	factors$PM$R39W = week.prices / mlag(week.prices, 39)

	#51 Week Volume Price Trend
	# compute weekly volume
	temp = bt.apply(data, function(x) cumsum(ifna(Vo(x),0)))
	temp = temp[week.ends,]
		week.volume = temp - mlag(temp)		
	temp = (week.prices - mlag(week.prices)) * week.volume
	factors$PM$VPT51W = bt.apply.matrix(temp, runSum, 51)

	# Convert weekly to daily
	for(i in 1:len(factors$PM)) {
		temp = prices * NA
		temp[week.ends,] = factors$PM[[i]]
		factors$PM[[i]] = bt.apply.matrix(temp, function(x) ifna.prev(x))
	}

	#Percent Above 260 Day Low
	factors$PM$P260LOW = prices / bt.apply.matrix(prices, runMin, 260)

	# Flip sign
	for(i in names(factors$PM)) factors$PM[[i]] = -factors$PM[[i]]

	#*****************************************************************
	# Create Price Reversal
	#****************************************************************** 
	factors$PR = list()
	factor.names$PR = 'Price Reversal'	

	#5 Day Industry Relative Return
	factors$PR$r5DR = prices/mlag(prices, 5)
		factors$PR$r5DR = factors$PR$r5DR / sector.mean(factors$PR$r5DR, sectors)

	#5 Day Money Flow / Volume
	factors$PR$MFV = bt.apply(data, function(x) {
		MFI(cbind(ifna.prev(Hi(x)),ifna.prev(Lo(x)),ifna.prev(Cl(x))), 5) / ifna.prev(Vo(x))
	})

	#10 Day MACD - Signal Line
	factors$PR$MACD = bt.apply.matrix(prices, function(x) {
		temp=MACD(x, 10)
		temp[, 'macd'] - temp[, 'signal']
		})		

	#14 Day RSI (Relative Strength Indicator)
	factors$PR$RSI = bt.apply.matrix(prices, RSI, 14)

	#14 Day Stochastic
	factors$PR$STOCH = bt.apply(data, function(x) {
		stoch(cbind(ifna.prev(Hi(x)),ifna.prev(Lo(x)),ifna.prev(Cl(x))),14)[,'slowD']
	})

	#4 Week Industry Relative Return
	factors$PR$rR4W = week.prices / mlag(week.prices,4)
		factors$PR$rR4W = factors$PR$rR4W / sector.mean(factors$PR$rR4W, sectors)

		# Convert weekly to daily
		temp = prices * NA
		temp[week.ends,] = factors$PR$rR4W
		factors$PR$rR4W = bt.apply.matrix(temp, function(x) ifna.prev(x))

	# VOMO - Volume x Momentum
	volume = bt.apply(data, function(x) ifna.prev(Vo(x)))
	factors$PR$VOMO = (prices / mlag(prices,10) - 1) * bt.apply.matrix(volume, runMean, 22) / bt.apply.matrix(volume, runMean, 66)

	# Flip sign
	for(i in names(factors$PR)) factors$PR[[i]] = -factors$PR[[i]]

	#*****************************************************************
	# Create Small Size
	#****************************************************************** 		
	factors$SS = list()
	factor.names$SS = 'Small Size'		

	#Log of Market Capitalization
	factors$SS$MC = log(MKVAL)

	#Log of Market Capitalization Cubed
	factors$SS$MC3 = log(MKVAL)³

	#Log of Stock Price
	factors$SS$P = log(prices)

	#Log of Total Assets
	factors$SS$AT = log(bt.apply(data, function(x) ifna.prev(x[, 'AT'])))

	#Log of Trailing-12-Month Sales
	factors$SS$SALE = log(bt.apply(data, function(x) ifna.prev(x[, 'SALE'])))

	# Flip sign
	for(i in names(factors$SS)) factors$SS[[i]] = -factors$SS[[i]]

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
			factors[[j]][[i]][] = ifna(factors[[j]][[i]],NA)
		}
	}

	#*****************************************************************
	# Create Relative Value
	#****************************************************************** 
	factors$RV = list()
	factor.names$RV = 'Relative Value'		

	# relative 
	for(i in spl('EP,SP,CFP')) {
		factors$RV[[paste('r',i,sep='')]] = factors$TV[[i]] / sector.mean(factors$TV[[i]], sectors) 		
	}

	# spreads, 5 Year Avg = 60 months
	for(i in spl('rEP,rSP,rCFP')) {
		factors$RV[[paste('s',i,sep='')]] = factors$RV[[i]] - 
		apply(factors$RV[[i]], 2, function(x) if(all(is.na(x))) x else SMA(x,60) )
	}

	#*****************************************************************
	# Profit Trends (Relative)
	#****************************************************************** 	
	# relative 
	for(i in spl('RS,SA')) {
		factors$PT[[paste('r',i,sep='')]] = factors$PT[[i]] / sector.mean(factors$PT[[i]], sectors)
	}			

```

接下来让我们创建复合平均因子并绘制其表现图。

```

	#*****************************************************************
	# Normalize and add Average factor
	#****************************************************************** 
	for(j in names(factors)) {
		factors[[j]] = normalize.normal(factors[[j]])
		factors[[j]] = add.avg.factor(factors[[j]])
	}

	#*****************************************************************
	# Create Composite Average factor
	#****************************************************************** 	
	factors.avg = list()
	for(j in names(factors)) factors.avg[[j]] = factors[[j]]$AVG

	factors.avg = add.avg.factor(factors.avg)

	#*****************************************************************
	# Backtest qutiles and qutile spread
	#****************************************************************** 
	plot.quantiles(factors.avg, next.month.ret, 'Average')

	plot.bt.quantiles(factors.avg$AVG, next.month.ret, 'Composite Average', data)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/02/plot1-small1.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/02/plot2-small2.png)

请注意，我在整个历史上都使用当前的道琼斯指数成分。这是一个问题，因为在过去 20 年中，道琼斯指数的构成已经多次变化。这种偏差的一个迹象是小型规模因子的高散布。低价股票和高价股票交易不一定会一直赚钱；但是如果我们事先知道低价公司将成为道琼斯指数的一部分，这是有道理的。

我们不是简单地对所有因子的平均值来对股票进行排名，而是可以运行横截面回归来估计因子载荷，并使用估计的因子载荷创建 Alpha 模型。关于这一过程的完整描述，我推荐阅读 R. Haugen, N. Baker (1996)的[《Expected Stock Returns 的确定因素》](http://www.quantitativeinvestment.com/documents/common.pdf)第 8-9 页。

```

	#*****************************************************************
	# Save CSFB factors to be used later to create multiple factor Risk Model
	#****************************************************************** 
	save(data, sectors, factors.avg, next.month.ret, file='data.factors.Rdata')
		# remove Composite Average factor
		factors.avg = factors.avg[which(names(factors.avg) != 'AVG')]

	#*****************************************************************
	# Run cross sectional regression and create Alpha model
	#****************************************************************** 
	nperiods = nrow(next.month.ret)
	n = ncol(next.month.ret)

	# create matrix for each factor
	factors.matrix = abind(factors.avg, along = 3)	
	all.data = factors.matrix

	# betas
	beta = all.data[,1,] * NA

	# append next.month.ret to all.data			
	all.data = abind(next.month.ret, all.data, along = 3)
		dimnames(all.data)[[3]][1] = 'Ret'

	# estimate betas (factor returns)
	for(t in 12:(nperiods-1)) {
		temp = all.data[t:t,,]
		x = temp[,-1]
		y = temp[,1]
		beta[(t+1),] = lm(y~x-1)$coefficients
	}

	# create Alpha return forecasts
	alpha = next.month.ret * NA

	for(t in 18:(nperiods-1)) {
		# average betas over the last 6 months
		coef = colMeans(beta[(t-5):t,],na.rm=T)
		alpha[t,] = rowSums(all.data[t,,-1] * t(repmat(coef, 1,n)), na.rm=T)	
	}

	#*****************************************************************
	# Backtest qutiles and qutile spread
	#****************************************************************** 
	layout(1:2)
	temp = compute.quantiles(alpha, next.month.ret, plot=T)
	plot.bt.quantiles(alpha, next.month.ret, 'Alpha', data)

```

![plot3.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/02/plot3-small.png)

回归模型的表现滞后于所有因子简单平均值对股票进行排名的表现。这可能有多种原因，但我想向您展示一种快速且合理的方法来提高回归模型的表现。

在回归过程中，我们不对估计的因子载荷进行限制；然而，对于价值因子来说，负系数是没有意义的。我不想明确地说好的价值公司应该比差的价值公司排名低，仅仅因为价值因子有一个负系数。一个可能的解决方案是只使用正因子载荷来构建 Alpha 得分。以下是修改后的代码：

```

	for(t in 18:(nperiods-1)) {
		# average betas over the last 6 months
		coef = colMeans(beta[(t-5):t,],na.rm=T)

		coef = iif(coef > 0, coef, 0)

		alpha[t,] = rowSums(all.data[t,,-1] * t(repmat(coef, 1,n)), na.rm=T)	
	}

```

![plot4.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/02/plot4-small.png)

回归模型仍然滞后于所有因子简单平均值对股票进行排名的表现。

在下一篇文章中，我将介绍如何创建一个风险模型并估计风险。

要查看此示例的完整源代码，请查看[github 上的 fm.all.factor.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/factor.model.test.r)。
