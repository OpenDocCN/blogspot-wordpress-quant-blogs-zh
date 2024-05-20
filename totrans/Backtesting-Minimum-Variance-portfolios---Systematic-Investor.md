<!--yml
category: 未分类
date: 2024-05-18 14:38:43
-->

# Backtesting Minimum Variance portfolios | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2011/12/13/backtesting-minimum-variance-portfolios/#0001-01-01](https://systematicinvestor.wordpress.com/2011/12/13/backtesting-minimum-variance-portfolios/#0001-01-01)

I want to show how to combine various risk measures I discussed while writing the series of posts about [Asset Allocation](https://systematicinvestor.wordpress.com/category/asset-allocation/) with backtesting library in the [Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/). I will use Minimum Variance portfolio as an example for this post.

I recommend reading a good discussion about Minimum Variance portfolios at [Minimum Variance Sector Rotation](http://quantivity.wordpress.com/2011/04/20/minimum-variance-sector-rotation/) post by Quantivity.

I will use the investment universe and rebalancing schedule as outlined in the [Forecast-Free Algorithms: A New Benchmark For Tactical Strategies](http://cssanalytics.wordpress.com/2011/08/09/forecast-free-algorithms-a-new-benchmark-for-tactical-strategies/) post by David Varadi. The investment universe:

| 1\. S&P500 ([SPY](http://www.google.com/finance?q=SPY)) |
| 2\. Nasdaq 100 ([QQQ](http://www.google.com/finance?q=QQQ)) |
| 3\. Emerging Markets ([EEM](http://www.google.com/finance?q=EEM)) |
| 4\. Russell 2000 ([IWM](http://www.google.com/finance?q=IWM)) |
| 5\. MSCI EAFE ([EFA](http://www.google.com/finance?q=EFA)) |
| 6\. Long-term Treasury Bonds ([TLT](http://www.google.com/finance?q=TLT)) |
| 7\. Real Estate ([IYR](http://www.google.com/finance?q=IYR)) |
| 8\. Gold ([GLD](http://www.google.com/finance?q=GLD)) |

The rebalancing is done on a weekly basis and quarterly data is used to estimate input assumptions.

Following code implements this strategy using the backtesting library in the [Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/):

```

# Load Systematic Investor Toolbox (SIT)
setInternet2(TRUE)
con = gzcon(url('https://github.com/systematicinvestor/SIT/raw/master/sit.gz', 'rb'))
	source(con)
close(con)

	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod,quadprog,lpSolve')
	tickers = spl('SPY,QQQ,EEM,IWM,EFA,TLT,IYR,GLD')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)

	data.weekly <- new.env()
		for(i in tickers) data.weekly[[i]] = to.weekly(data[[i]], indexAt='endof')

	bt.prep(data, align='remove.na', dates='1990::2011')
	bt.prep(data.weekly, align='remove.na', dates='1990::2011')

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 
	prices = data$prices   
	n = ncol(prices)

	# find week ends
	week.ends = endpoints(prices, 'weeks')
		week.ends = week.ends[week.ends > 0]		

	# Equal Weight 1/N Benchmark
	data$weight[] = NA
		data$weight[week.ends,] = ntop(prices[week.ends,], n)		

		capital = 100000
		data$weight[] = (capital / prices) * data$weight
	equal.weight = bt.run(data, type='share')

	#*****************************************************************
	# Create Constraints
	#*****************************************************************
	constraints = new.constraints(n, lb = -Inf, ub = +Inf)

	# SUM x.i = 1
	constraints = add.constraints(rep(1, n), 1, type = '=', constraints)		

	ret = prices / mlag(prices) - 1
	weight = coredata(prices)
		weight[] = NA

	for( i in week.ends[week.ends >= (63 + 1)] ) {
		# one quarter is 63 days
		hist = ret[ (i- 63 +1):i, ]

		# create historical input assumptions
		ia = create.historical.ia(hist, 252)
			s0 = apply(coredata(hist),2,sd)		
			ia$cov = cor(coredata(hist), use='complete.obs',method='pearson') * (s0 %*% t(s0))

		weight[i,] = min.risk.portfolio(ia, constraints)
	}

	# Minimum Variance
	data$weight[] = weight		
		capital = 100000
		data$weight[] = (capital / prices) * data$weight
	min.var.daily = bt.run(data, type='share', capital=capital)

```

Next let’s create Minimum Variance portfolios using weekly data:

```

	#*****************************************************************
	# Code Strategies: Weekly
	#****************************************************************** 	
	retw = data.weekly$prices / mlag(data.weekly$prices) - 1
	weightw = coredata(prices)
		weightw[] = NA

	for( i in week.ends[week.ends >= (63 + 1)] ) {	
		# map
		j = which(index(ret[i,]) == index(retw))

		# one quarter = 13 weeks
		hist = retw[ (j- 13 +1):j, ]

		# create historical input assumptions
		ia = create.historical.ia(hist, 52)
			s0 = apply(coredata(hist),2,sd)		
			ia$cov = cor(coredata(hist), use='complete.obs',method='pearson') * (s0 %*% t(s0))

		weightw[i,] = min.risk.portfolio(ia, constraints)
	}	

	data$weight[] = weightw		
		capital = 100000
		data$weight[] = (capital / prices) * data$weight
	min.var.weekly = bt.run(data, type='share', capital=capital)

	#*****************************************************************
	# Create Report
	#****************************************************************** 
	plotbt.custom.report.part1(min.var.weekly, min.var.daily, equal.weight)

	# plot Daily and Weekly transition maps
	layout(1:2)
	plotbt.transition.map(min.var.daily$weight)
		legend('topright', legend = 'min.var.daily', bty = 'n')
	plotbt.transition.map(min.var.weekly$weight)
		legend('topright', legend = 'min.var.weekly', bty = 'n')

```

[![](img/1e8fa5169596dc6cdaae707627e72d45.png "plot1.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot1-small2.png)

[![](img/cf20676b6db5c6fcf5de8d6f6896df5e.png "plot2.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot2-small2.png)

[![](img/d9508b3598d8e7eb5b566165f820552f.png "plot3.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot3-small2.png)

I find it very interesting that the Minimum Variance portfolios constructed using daily returns to create input assumptions are way different from the Minimum Variance portfolios constructed using weekly returns to create input assumptions. One possible explanation for this discrepancy was examined by Pat Burns in the [The volatility mystery continues](http://www.portfolioprobe.com/2011/12/05/the-volatility-mystery-continues/) post.

There are a few ways I suggest you can play with this code:

*   make covariance matrix estimate more stable, use the Ledoit-Wolf covariance shrinkage estimator from tawny package

    ```

    ia$cov = tawny::cov.shrink(hist)

    ```

    or

    ```

    ia$cov = cor(coredata(hist), use='complete.obs',method='spearman') * (s0 %*% t(s0))

    ```

    or

    ```

    ia$cov = cor(coredata(hist), use='complete.obs',method='kendall') * (s0 %*% t(s0))

    ```

*   use different investment universe
*   consider different rebalancing schedule
*   consider different risk measures. for example, I discussed and implemented following risk measures in the series of posts about [Asset Allocation](https://systematicinvestor.wordpress.com/category/asset-allocation/):
    *   min.maxloss.portfolio
    *   min.mad.portfolio
    *   min.cvar.portfolio
    *   min.cdar.portfolio
    *   min.mad.downside.portfolio
    *   min.risk.downside.portfolio

To view the complete source code for this example, please have a look at the [bt.min.var.test() function in bt.test.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r).