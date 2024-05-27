<!--yml

类别：未分类

日期：2024-05-18 14:31:38

-->

# 佣金 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2013/11/05/commissions/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/11/05/commissions/#0001-01-01)

今天，我想解释一下内置于[Systematic Investor Toolbox(SIT)](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)的“share”回测中的佣金功能。

在每次重新平衡时，资金根据权重分配，以使

```

	share = weight * capital / price
	cash  = capital - share * price

```

例如，如果权重为 100%（即全部投资）且资金= $100 且价格= $10，则

```

	share = 10 shares
	cash = $0

```

期间收益等于

```

	return = [share * price + cash] / [share * price.yesterday + cash] - 1

```

总回报等于

```

	total.return = [1 + return.0] * [1 + return.1] * ... * [1 + return.n] - 1

```

以这种方式构造的期间收益使我能够构造投资组合收益而不使用循环

即如果 share、price、cash 是矩阵，则

```

	portfolio.return = rowSums((share * price + cash) / (share * mlag(price) + cash) - 1)

```

和

```

	equity = cumprod(1 + portfolio.return)

```

为了将佣金引入上述框架，我必须做出以下假设。

假设 P0 和 P1 是股票价格，com 是与股票价格相比非常小的佣金，则

```

	[P0 - com] / P0 is close (equal) to P0 / [P0 + com] and
	[P0 - com] * P1 is close (equal) to P0 * [P1 - com]

```

给定佣金，[SIT](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)中使用的期间回报公式等于

```

	return = [share * price + cash - commission] / [share * price.yesterday + cash] - 1

```

现在让我们看一个带有佣金的交易示例：

```

	Let's say we are fully invested (i.e. cash = 0 and capital = share * P0)

	opening trade cost = share * P0 + com
	closing  trade cost = share * P1 - com

	return = [closing  trade cost] / [opening trade cost] - 1
	= [share * P1 - com] / [share * P0 + com] - 1

```

在[SIT](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)中，这些计算等效于

```

	([capital - com] / [capital]) * ([share * P1 + cash - com] / [share * P0 + cash]) - 1

	< given that cash = 0 and capital = share * P0 >
	= ([share * P0 - com] / [share * P0]) * ([share * P1 - com] / [share * P0]) - 1

	< given [P0 - com] / P0 ~ P0 / [P0 + com] >
	= ([share * P0] / [share * P0 + com] / ) * ([share * P1 - com] / [share * P0]) - 1

	= [share * P1 - com] / [share * P0 + com] - 1

```

因此，只要佣金相对于整个交易很小，使用[SIT](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)生成的回报将非常接近真实回报。

SIT 目前支持以下 3 种类型的佣金

+   每股收费

    ```

    	commission = abs(share - mlag(share)) * commission$cps

    ```

+   固定佣金

    ```

    	commission = sign(abs(share - mlag(share))) * commission$fixed

    ```

+   百分比佣金

    ```

    	commission = price * abs(share - mlag(share)) * commission$percentage

    ```

你可以以任何方式混合匹配这些佣金方法，

```

	the total.commission = cps.commission + fixed.commission + percentage.commission

```

期间回报等于

```

	return = (share * price + cash - total.commission) / (share * mlag(price) + cash) - 1

```

接下来让我们看看不同类型佣金的影响。 有两种指定佣金的方式。

+   ```
    commission = 0.1
    ```

    将被翻译为

    ```
    commission = list(cps = 0.1, fixed = 0.0, percentage = 0.0)
    ```

+   ```
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

要查看此示例的完整源代码，请查看[github 上的 bt.test.r 中的 bt.commission.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
