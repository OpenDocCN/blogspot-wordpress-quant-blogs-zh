<!--yml
category: 未分类
date: 2024-05-18 14:31:38
-->

# Commissions | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2013/11/05/commissions/#0001-01-01](https://systematicinvestor.wordpress.com/2013/11/05/commissions/#0001-01-01)

Today, I want to explain the commission’s functionality build in to [Systematic Investor Toolbox(SIT)](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/) “share” back-test.

At each re-balance time the capital is allocated given the weight such that

```

	share = weight * capital / price
	cash  = capital - share * price

```

For example, if weight is 100% (i.e. fully invested) and capital = $100 and price = $10 then

```

	share = 10 shares
	cash = $0

```

The period return is equal to

```

	return = [share * price + cash] / [share * price.yesterday + cash] - 1

```

The total return is equal to

```

	total.return = [1 + return.0] * [1 + return.1] * ... * [1 + return.n] - 1

```

The period returns constructed this way let me construct portfolio returns without using loops
I.e. if share, price, cash are matrices, then

```

	portfolio.return = rowSums((share * price + cash) / (share * mlag(price) + cash) - 1)

```

and

```

	equity = cumprod(1 + portfolio.return)

```

To introduce commissions into above framework, I had to make following assumptions.
Let’ assume that P0 and P1 are stock prices and com is commission that is very small relative to stock price then

```

	[P0 - com] / P0 is close (equal) to P0 / [P0 + com] and
	[P0 - com] * P1 is close (equal) to P0 * [P1 - com]

```

Given commissions, the period return formula used in [SIT](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/) is equal to

```

	return = [share * price + cash - commission] / [share * price.yesterday + cash] - 1

```

Now let’s look at the example of trade with commissions:

```

	Let's say we are fully invested (i.e. cash = 0 and capital = share * P0)

	opening trade cost = share * P0 + com
	closing  trade cost = share * P1 - com

	return = [closing  trade cost] / [opening trade cost] - 1
	= [share * P1 - com] / [share * P0 + com] - 1

```

In [SIT](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/), these computations are equivalent to

```

	([capital - com] / [capital]) * ([share * P1 + cash - com] / [share * P0 + cash]) - 1

	< given that cash = 0 and capital = share * P0 >
	= ([share * P0 - com] / [share * P0]) * ([share * P1 - com] / [share * P0]) - 1

	< given [P0 - com] / P0 ~ P0 / [P0 + com] >
	= ([share * P0] / [share * P0 + com] / ) * ([share * P1 - com] / [share * P0]) - 1

	= [share * P1 - com] / [share * P0 + com] - 1

```

Hence, as long as commissions are small relative to whole trade the returns produced with [SIT](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/) will be very close to the true returns.

SIT currently supports following 3 types of commissions

*   cents / share commission

    ```

    	commission = abs(share - mlag(share)) * commission$cps

    ```

*   fixed commission

    ```

    	commission = sign(abs(share - mlag(share))) * commission$fixed

    ```

*   percentage commission

    ```

    	commission = price * abs(share - mlag(share)) * commission$percentage

    ```

You can mix and match these commission methods in any way,

```

	the total.commission = cps.commission + fixed.commission + percentage.commission

```

and period return is equal to

```

	return = (share * price + cash - total.commission) / (share * mlag(price) + cash) - 1

```

Next let’s see the impact of different type of commissions. There two ways to specify the commissions.

*   ```
    commission = 0.1
    ```

    will be translated in

    ```
    commission = list(cps = 0.1, fixed = 0.0, percentage = 0.0)
    ```

*   ```
    commission = list(cps = 0.0, fixed = 0.0, percentage = 0.0)
    ```

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
	tickers = spl('EEM')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)			
	bt.prep(data, align='keep.all', dates='2013:08::2013:09')	

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 		
	buy.date = '2013:08:14'	
	sell.date = '2013:08:15'
	day.after.sell.date = '2013:08:16'		

	capital = 100000
	prices = data$prices
	share = as.double(capital / prices[buy.date])

	# helper function to compute trade return
	comp.ret <- function(sell.trade.cost, buy.trade.cost) { round(100 * (as.double(sell.trade.cost) / as.double(buy.trade.cost) - 1), 2) }

	#*****************************************************************
	# Zero commission
	#****************************************************************** 
	data$weight[] = NA
		data$weight[buy.date] = 1
		data$weight[sell.date] = 0
		commission = 0.0
	model = bt.run.share(data, commission = commission, capital = capital, silent = T)

	comp.ret( share * prices[sell.date], share * prices[buy.date] )		
	comp.ret( model$equity[day.after.sell.date], model$equity[buy.date] )		

	#*****************************************************************
	# 10c cps commission
	# cents / share commission
   	#   trade cost = abs(share - mlag(share)) * commission$cps	
	#****************************************************************** 
	data$weight[] = NA
		data$weight[buy.date] = 1
		data$weight[sell.date] = 0
		commission = 0.1
	model = bt.run.share(data, commission = commission, capital = capital, silent = T)

	comp.ret( share * (prices[sell.date] - commission), share * (prices[buy.date] + commission) )
	comp.ret( model$equity[day.after.sell.date], model$equity[buy.date] )		

	#*****************************************************************
	# $5 fixed commission
	# fixed commission per trade to more effectively to penalize for turnover
   	#   trade cost = sign(abs(share - mlag(share))) * commission$fixed	
	#****************************************************************** 
	data$weight[] = NA
		data$weight[buy.date] = 1
		data$weight[sell.date] = 0
		commission = list(cps = 0.0, fixed = 5.0, percentage = 0.0)	
	model = bt.run.share(data, commission = commission, capital = capital, silent = T)

	comp.ret( share * prices[sell.date] - commission$fixed, share * prices[buy.date] + commission$fixed )
	comp.ret( model$equity[day.after.sell.date], model$equity[buy.date] )		

	#*****************************************************************
	# % commission
	# percentage commission
	#   trade cost = price * abs(share - mlag(share)) * commission$percentage	
	#****************************************************************** 
	data$weight[] = NA
		data$weight[buy.date] = 1
		data$weight[sell.date] = 0
		commission = list(cps = 0.0, fixed = 0.0, percentage = 1/100)	
	model = bt.run.share(data, commission = commission, capital = capital, silent = T)

	comp.ret( share * prices[sell.date] * (1 - commission$percentage), share * prices[buy.date] * (1 + commission$percentage) )
	comp.ret( model$equity[day.after.sell.date], model$equity[buy.date] )	

```

To view the complete source code for this example, please have a look at the [bt.commission.test() function in bt.test.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r).