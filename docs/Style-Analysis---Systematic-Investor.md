<!--yml

类别：未分类

日期：2024-05-18 14:45:51

-->

# 风格分析 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2011/11/18/style-analysis/#0001-01-01`](https://systematicinvestor.wordpress.com/2011/11/18/style-analysis/#0001-01-01)

在资产分配过程的最后阶段，我们必须决定如何实施我们的理想分配。在许多情况下，我们将资本分配给基金经理，他们将根据基金的投资方针投资资金。通常资产类别和基金经理之间没有完美的关系。为了确定经理的真实风格，可以检查其历史持仓或进行风格分析。风格分析是一个试图将基金表现归因于资产类别表现的过程，通过运行受约束的线性回归。对于风格分析的详细审查，我推荐阅读以下文章：

我想 examine [Fidelity Worldwide Fund (FWWFX)](http://fundresearch.fidelity.com/mutual-funds/summary/315910505) 的风格。首先，让我们从 [Yahoo Fiance](http://finance.yahoo.com) 获取历史基金和资产类别价格：

```

# load Systematic Investor Toolbox
setInternet2(TRUE)
source(gzcon(url('https://github.com/systematicinvestor/SIT/raw/master/sit.gz', 'rb')))

	#--------------------------------------------------------------------------
	# Get Historical Data
	#--------------------------------------------------------------------------
	load.packages('quantmod')

	# load historical prices from Yahoo Finance
	symbols = spl('FWWFX,EWA,EWC,EWQ,EWG,EWJ,EWU,SPY')		
	symbol.names = spl('Fund,Australia,Canada,France,Germany,Japan,UK,USA')	
	getSymbols(symbols, from = '1980-01-01', auto.assign = TRUE)

	# align dates for all symbols & convert to frequency 
	hist.prices = merge(FWWFX,EWA,EWC,EWQ,EWG,EWJ,EWU,SPY)		
		period.ends = endpoints(hist.prices, 'months')
		hist.prices = Ad(hist.prices)[period.ends, ]

		index(hist.prices) = as.Date(paste('1/', format(index(hist.prices), '%m/%Y'), sep=''), '%d/%m/%Y')
		colnames(hist.prices) = symbol.names

	# remove any missing data	
	hist.prices = na.omit(hist.prices['1990::2010'])

	# compute simple returns	
	hist.returns = na.omit( ROC(hist.prices, type = 'discrete') )

	#load 3-Month Treasury Bill from FRED
	TB3M = quantmod::getSymbols('TB3MS', src='FRED', auto.assign = FALSE)	
	TB3M = processTBill(TB3M, timetomaturity = 1/4)
		index(TB3M) = as.Date(paste('1/', format(index(TB3M), '%m/%Y'), sep=''), '%d/%m/%Y')
		TB3M = ROC(Ad(TB3M), type = 'discrete')
		colnames(TB3M) = 'Cash'

	# add Cash to the asset classes
	hist.returns = na.omit( merge(hist.returns, TB3M) )

```

为了确定 Fidelity Worldwide Fund 的风格，我将运行一个回归模型，在滚动 36 个月窗口期内，将基金回报对国家资产类别进行回归。首先，让我们天真地运行回归，不施加任何约束：

```

	#--------------------------------------------------------------------------
	# Style Regression over 36 Month window, unconstrained
	#--------------------------------------------------------------------------
	# setup
	ndates = nrow(hist.returns)
	n = ncol(hist.returns)-1
	window.len = 36

	style.weights = hist.returns[, -1]
		style.weights[] = NA
	style.r.squared = hist.returns[, 1]
		style.r.squared[] = NA

	# main loop
	for( i in window.len:ndates ) {
		window.index = (i - window.len + 1) : i

		fit = lm.constraint( hist.returns[window.index, -1], hist.returns[window.index, 1] )	
			style.weights[i,] = fit$coefficients
			style.r.squared[i,] = fit$r.squared
	}

	# plot 
	aa.style.summary.plot('Style UnConstrained', style.weights, style.r.squared, window.len)

```

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot1-small7.png)

分配起起伏伏没有 consistent fashion。回归 also 表明基金使用了 leverage (即 Cash -171%)，这并不是 case。为 fix 这些问题，我将 introduce 以下约束：

+   所有风格权重都在 0% 和 100% 之间。

+   风格权重之和等于 100%。

```

	#--------------------------------------------------------------------------
	# Style Regression over Window, constrained
	#--------------------------------------------------------------------------
	# setup
	load.packages('quadprog')

	style.weights[] = NA
	style.r.squared[] = NA

	# Setup constraints
	# 0 <= x.i <= 1
	constraints = new.constraints(n, lb = 0, ub = 1)

	# SUM x.i = 1
	constraints = add.constraints(rep(1, n), 1, type = '=', constraints)		

	# main loop
	for( i in window.len:ndates ) {
		window.index = (i - window.len + 1) : i

		fit = lm.constraint( hist.returns[window.index, -1], hist.returns[window.index, 1], constraints )	
			style.weights[i,] = fit$coefficients
			style.r.squared[i,] = fit$r.squared
	}

	# plot	
	aa.style.summary.plot('Style Constrained', style.weights, style.r.squared, window.len)

```

![plot2.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot2-small6.png)

引入约束后，分配更稳定，但历史美国分配（用黄色突出显示）从 2000 年的 0% 波动到 2006 年的 60%。这非常可疑，唯一检查这是否属实的 way 是查看基金备忘录和持仓。现在，我假设资产类别分配可以围绕当前基金分配 vary。为获取当前基金分配，我将检查其当前持仓于：

我施加了额外的下限和上限约束：

```

	#--------------------------------------------------------------------------
	# Style Regression  over Window, constrained + limits on allocation
	#--------------------------------------------------------------------------
	# setup
	style.weights[] = NA
	style.r.squared[] = NA

	# Setup constraints
	temp = rep(0, n)
		names(temp) = colnames(hist.returns)[-1]
	lb = temp
	ub = temp
	ub[] = 1

	lb['Australia'] = 0
	ub['Australia'] = 5

	lb['Canada'] = 0
	ub['Canada'] = 5

	lb['France'] = 0
	ub['France'] = 15

	lb['Germany'] = 0
	ub['Germany'] = 15

   	lb['Japan'] = 0
	ub['Japan'] = 15

   	lb['UK'] = 0
	ub['UK'] = 25

   	lb['USA'] = 30
	ub['USA'] = 100

   	lb['Cash'] = 2
	ub['Cash'] = 15

	# 0 <= x.i <= 1
	constraints = new.constraints(n, lb = lb/100, ub = ub/100)

	# SUM x.i = 1
	constraints = add.constraints(rep(1, n), 1, type = '=', constraints)		

	# main loop
	for( i in window.len:ndates ) {
		window.index = (i - window.len + 1) : i

		fit = lm.constraint( hist.returns[window.index, -1], hist.returns[window.index, 1], constraints )	
			style.weights[i,] = fit$coefficients
			style.r.squared[i,] = fit$r.squared
	}

	# plot
	aa.style.summary.plot('Style Constrained+Limits', style.weights, style.r.squared, window.len)

```

![plot3.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot3-small4.png)

最后的风格分配看起来更有可能。如果历史基金持仓 readily available 我们，我们就可以 examine 它们来 refine 上下边界。最后一步是分析基金实际回报 vs 风格矩阵暗示的回报。

```

	#--------------------------------------------------------------------------
	# Look at Manager's Tracking Error
	#--------------------------------------------------------------------------
	manager.returns = hist.returns[, 1]
		manager.returns = manager.returns[window.len:ndates,]
	implied.returns = as.xts( rowSums(style.weights * hist.returns[, -1]), index(hist.returns))
		implied.returns = implied.returns[window.len:ndates,]

	tracking.error = manager.returns - implied.returns
	alpha = 12*mean(tracking.error)
	covar.alpha = 12* cov(tracking.error)

	# plot
	layout(1:2)
	plota(cumprod(1+manager.returns), type='l')
		plota.lines(cumprod(1+implied.returns), col='red')
		plota.legend('Fund,Style', 'black,red')

	par(mar = c(4,4,2,1))
	hist(100*tracking.error, xlab='Monthly Tracking Error',
		main= paste('Annualized Alpha =', round(100*alpha,1), 'Std Dev =', round(100*sqrt(covar.alpha),1))
	)

```

请参考附件中的[图片](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot4-small2.png)。

在过去十年中，富达全球基金的表现一直优于其代理，这一点从风格矩阵中可以看出。该基金的 alpha 收益为 2.9%，alpha 收益的标准差为 3.9%。所以，如果你想投资全球基金，富达全球基金是一个不错的选择。

要查看此示例的完整源代码，请查看 github 上的 [aa.style.test() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/aa.test.r)。
