<!--yml

类别：未分类

日期：2024-05-18 14:36:24

-->

# 模型化懒人投资策略 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/10/26/modeling-couch-potato-strategy/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/10/26/modeling-couch-potato-strategy/#0001-01-01)

我第一次在《金钱感觉》杂志上读到[懒人投资策略](http://www.moneysense.ca/2006/04/05/couch-potato-portfolio-introduction/)。我喜欢这个简单的策略，因为它容易理解，也容易管理。 [懒人投资策略](http://www.moneysense.ca/2006/04/05/couch-potato-portfolio-introduction/)与我之前分析过的[永久投资组合策略](https://systematicinvestor.wordpress.com/?s=Permanent+Portfolio)类似。

[懒人投资策略](http://www.moneysense.ca/2006/04/05/couch-potato-portfolio-introduction/)将资金按照给定的比例投资于不同类型的资产以确保多样化，并每年平衡一次持仓。例如，[经典懒人投资策略](http://www.moneysense.ca/2006/04/05/couch-potato-portfolio-meet-the-potato-family/)是：

+   1) 加拿大股票（33.3%）

+   2) 美国股票（33.3%）

+   3) 加拿大债券（33.3%）

我强烈推荐阅读以下在线资源以获取更多关于[懒人投资策略](http://www.moneysense.ca/2006/04/05/couch-potato-portfolio-introduction/)的信息：

+   金钱感觉

+   加拿大懒人投资组合

+   资产构建器

今天，我想展示如何使用[系统投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)来模拟和监控[懒人投资策略](http://www.moneysense.ca/2006/04/05/couch-potato-portfolio-introduction/)。

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)
# https://systematicinvestor.wordpress.com/systematic-investor-toolbox/
###############################################################################
setInternet2(TRUE)
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

	# helper function to model Couch Potato strategy - a fixed allocation strategy
	couch.potato.strategy <- function
	(
		data.all,
		tickers = 'XIC.TO,XSP.TO,XBB.TO',
		weights = c( 1/3, 1/3, 1/3 ), 		
		periodicity = 'years',
		dates = '1900::',
		commission = 0.1
	) 
	{ 
		#*****************************************************************
		# Load historical data 
		#****************************************************************** 
		tickers = spl(tickers)
		names(weights) = tickers

		data <- new.env()
		for(s in tickers) data[[ s ]] = data.all[[ s ]]

		bt.prep(data, align='remove.na', dates=dates)

		#*****************************************************************
		# Code Strategies
		#******************************************************************
		prices = data$prices   
			n = ncol(prices)
			nperiods = nrow(prices)

		# find period ends
		period.ends = endpoints(data$prices, periodicity)
			period.ends = c(1, period.ends[period.ends > 0])

		#*****************************************************************
		# Code Strategies
		#******************************************************************
		data$weight[] = NA
			for(s in tickers) data$weight[period.ends, s] = weights[s]
		model = bt.run.share(data, clean.signal=F, commission=commission)

		return(model)
	} 	

```

懒人.potato.strategy()函数为给定的静态分配创建了一个定期平衡的投资组合。

接下来，让我们回测一些加拿大的懒人投资组合：

```

	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')	
	map = list()
		map$can.eq = 'XIC.TO'
		map$can.div = 'XDV.TO'		
		map$us.eq = 'XSP.TO'
		map$us.div = 'DVY'			
		map$int.eq = 'XIN.TO'		
		map$can.bond = 'XBB.TO'
		map$can.real.bond = 'XRB.TO'
		map$can.re = 'XRE.TO'		
		map$can.it = 'XTR.TO'
		map$can.gold = 'XGD.TO'

	data <- new.env()
	for(s in names(map)) {
		data[[ s ]] = getSymbols(map[[ s ]], src = 'yahoo', from = '1995-01-01', env = data, auto.assign = F)
		data[[ s ]] = adjustOHLC(data[[ s ]], use.Adjusted=T)	
	}

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 
	models = list()
		periodicity = 'years'
		dates = '2006::'

	models$classic = couch.potato.strategy(data, 'can.eq,us.eq,can.bond', rep(1/3,3), periodicity, dates)
	models$global = couch.potato.strategy(data, 'can.eq,us.eq,int.eq,can.bond', c(0.2, 0.2, 0.2, 0.4), periodicity, dates)
	models$yield = couch.potato.strategy(data, 'can.div,can.it,us.div,can.bond', c(0.25, 0.25, 0.25, 0.25), periodicity, dates)
	models$growth = couch.potato.strategy(data, 'can.eq,us.eq,int.eq,can.bond', c(0.25, 0.25, 0.25, 0.25), periodicity, dates)

	models$complete = couch.potato.strategy(data, 'can.eq,us.eq,int.eq,can.re,can.real.bond,can.bond', c(0.2, 0.15, 0.15, 0.1, 0.1, 0.3), periodicity, dates)	

	models$permanent = couch.potato.strategy(data, 'can.eq,can.gold,can.bond', c(0.25,0.25,0.5), periodicity, dates)	

	#*****************************************************************
	# Create Report
	#****************************************************************** 
	plotbt.custom.report.part1(models)

```

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/10/plot1-small3.png)

我包含了一些经典懒人投资组合和永久投资组合的加拿大版本。股票曲线可以为自己说明：您可以称它们为花哨的名字，但最终懒人投资组合的所有变体在 2008 年的跌幅都很大。在 2008 年熊市中，永久投资组合表现得更好。

接下来，让我们回测一些美国的懒人投资组合：

```

	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	tickers = spl('VIPSX,VTSMX,VGTSX,SPY,TLT,GLD,SHY')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1995-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)	

		# extend GLD with Gold.PM - London Gold afternoon fixing prices
		data$GLD = extend.GLD(data$GLD)

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 
	models = list()
		periodicity = 'years'
		dates = '2003::'

	models$classic = couch.potato.strategy(data, 'VIPSX,VTSMX', rep(1/2,2), periodicity, dates)
	models$margarita = couch.potato.strategy(data, 'VIPSX,VTSMX,VGTSX', rep(1/3,3), periodicity, dates)
	models$permanent = couch.potato.strategy(data, 'SPY,TLT,GLD,SHY', rep(1/4,4), periodicity, dates)

	#*****************************************************************
	# Create Report
	#****************************************************************** 
	plotbt.custom.report.part1(models)

```

![plot2.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/10/plot2-small3.png)

美国的懒人投资组合在 2008 年也经历了巨大的跌幅。永久投资组合表现得更好。

关于土豆投资者策略已经有很多论述，但是当我查看不同的变体时，我真的看不到在绩效或回撤方面有太大差异。也许这就是为什么在过去的几年里，我看到了许多新的 ETF 的诞生，以一种或另一种方式解决这个问题。例如，现在我们有[战术资产配置 ETF](http://www.mebanefaber.com/2010/09/29/cambria-global-tactical-etf-nysegtaa/)、[最低波动率 ETF](http://www.invescopowershares.com/products/overview.aspx?ticker=SPLV)、[带有看涨期权覆盖的收益 ETF](http://www.moneysense.ca/2011/06/02/bmo-covered-call-canadian-banks-etf-zwb/)。

要查看此例的完整源代码，请查看[github 上 bt.test.r 文件中的 bt.couch.potato.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。

来自[加拿大土豆投资者](http://canadiancouchpotato.com/)博客的一些值得一读的附加参考资料：
