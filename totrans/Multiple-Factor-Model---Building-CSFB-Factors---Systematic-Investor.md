<!--yml
category: 未分类
date: 2024-05-18 14:42:58
-->

# Multiple Factor Model – Building CSFB Factors | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2012/02/13/multiple-factor-model-building-csfb-factors/#0001-01-01](https://systematicinvestor.wordpress.com/2012/02/13/multiple-factor-model-building-csfb-factors/#0001-01-01)

This is the third post in the series about Multiple Factor Models. I will build on the code presented in the prior post, [Multiple Factor Model – Building Fundamental Factors](https://systematicinvestor.wordpress.com/2012/02/04/multiple-factor-model-building-fundamental-factors/), and I will show how to build majority of factors described in the CSFB Alpha Factor Framework. For details of the CSFB Alpha Factor Framework please read [CSFB Quantitative Research, Alpha Factor Framework on page 11, page 49 by P. N. Patel, S. Yao, R. Carlson, A. Banerji, J. Handelman](http://www.scribd.com/mobile/documents/62210581/download?commit=Download+Now&secret_password=).

This post will include long sections of code to extract/format data and build factors. I created a few helper functions for data manipulations and visualizations in the [factor.model.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/factor.model.r). For example, consecutive.changes function counts the number of consecutive positive changes.

The outline of this post:

*   Create majority of CSFB factors
*   Create and test Composite Average factor
*   Run cross sectional regression to estimate factor loading
*   Create and test Alpha model using estimated factor loading

Let’s start by getting Fundamental data and creating factors. In the prior post, I mentioned that it takes a while to download historical fundamental data for all companies in the Dow Jones index, and I recommend saving fundamental data with save(data.fund, file=’data.fund.Rdata’) command. In the following code I will just load historical fundamental data with load(file=’data.fund.Rdata’) command instead of downloading all data again.

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

Next let’s create majority of CSFB factors.

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
	factors$SS$MC3 = log(MKVAL)^3

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

Next let’s create Composite Average factor and chart its performance.

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

[![](img/ca57aa43f968203c50f43d5bd2258cac.png "plot1.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/02/plot1-small1.png)

[![](img/16f8ddfa4c3c0c8393f0ab4c5c5f8e33.png "plot2.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/02/plot2-small2.png)

Please note that I’m using the current Dow Jones index components through out the whole history. This is a problem because the Dow Jones index changed its composition a few times in the last 20 years. One of the signs of this bias is high spread for Small Size group of factors. It is not obvious that buying low priced stocks and selling high priced stocks should consistently make money; but it makes sense, if we know beforehand that that low priced companies will be part of Dow Jones index at some point.

Instead of using a simple average of all factors to rank stocks, we can run cross sectional regression to estimate factor loading, and create Alpha model using estimated factor loading. For a complete description of this process, I recommend reading [Commonality In The Determinants Of Expected Stock Returns by R. Haugen, N. Baker (1996)](http://www.quantitativeinvestment.com/documents/common.pdf) pages 8-9.

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

[![](img/5b284732329e9996457fd518271e0605.png "plot3.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/02/plot3-small.png)

The performance of the regression model lags the performance of the simple average of all factors to rank stocks. There are might be many reasons for this, but I want to show you one quick and rational way to increase performance of the regression model.

We do not restrict estimated factor loadings during regression; however, a negative coefficient for a Value factor does not make sense. I don’t want explicitly say that good Value companies should have lower ranks than bad Value companies, just because there is a negative coefficient for a Value factor. One possible solution is to only use factor loadings that are positive to construct Alpha score. Here is the modified code:

```

	for(t in 18:(nperiods-1)) {
		# average betas over the last 6 months
		coef = colMeans(beta[(t-5):t,],na.rm=T)

		coef = iif(coef > 0, coef, 0)

		alpha[t,] = rowSums(all.data[t,,-1] * t(repmat(coef, 1,n)), na.rm=T)	
	}

```

[![](img/f80756c3bd3b4a3a57aac4dc276a1d4c.png "plot4.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/02/plot4-small.png)

The regression model still lags the performance of the simple average of all factors to rank stocks.

In the next post I will show how to create a risk model and estimate risk.

To view the complete source code for this example, please have a look at the [fm.all.factor.test() function in factor.model.test.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/factor.model.test.r).