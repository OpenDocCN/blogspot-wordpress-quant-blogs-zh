<!--yml

分类：未分类

日期：2024-05-18 14:45:01

-->

# 多资产回测：旋转交易策略 | 系统性投资者

> 来源：[`systematicinvestor.wordpress.com/2011/12/06/multi-asset-backtest-rotational-trading-strategies/#0001-01-01`](https://systematicinvestor.wordpress.com/2011/12/06/multi-asset-backtest-rotational-trading-strategies/#0001-01-01)

我想讨论使用系统性投资者工具箱中的回测库来实现旋转交易策略。旋转交易策略会在时间上调整投资分配，投注于少数顶级排名的资产。例如，排名可以基于相对强度或动量。旋转交易策略（或战术资产配置）的一些例子包括：

我想通过在 [ETF Sector Strategy](http://www.etfscreen.com/sectorstrategy.php) 帖子中介绍的 ETF 筛选策略来说明旋转交易。每个月，这个策略投资于按六个月回报率排序的 21 个 ETF 中的前两个。为了降低换手率，后续月份中只要这些 ETF 保持在前六名，就会保持这些 ETF 头寸。

在我们实施这个策略之前，我们需要创建两个辅助程序。首先，让我们创建一个函数，该函数将为每个时期选择 top N 头寸：

```

############################################################################### 
# Select top N for each period
############################################################################### 
ntop <- function
(
	data,		# matrix with observations
	topn = 1, 	# top n
	dirMaxMin = TRUE
) 
{
	out = data
	out[] = NA

	for( i in 1:nrow(data) ) {
		x = coredata(data[i,])
		o = sort.list(x, na.last = TRUE, decreasing = dirMaxMin)
		index = which(!is.na(x))
		x[] = NA

		if(len(index)>0) {
			n = min(topn, len(index))
			x[o[1:n]] = 1/n
		}
		out[i,] = x
	}
	out[is.na(out)] = 0	
	return( out )
}

```

接下来，让我们创建一个函数，该函数将为每个时期选择 top N 头寸，并在它们跌出 KeepN 排名之前保持它们：

```

############################################################################### 
# Select top N for each period, and keep them till they drop below keepn rank
############################################################################### 
ntop.keep <- function
(
	data, 		# matrix with observations
	topn = 1, 	# top n
	keepn = 1, 	# keep n
	dirMaxMin = TRUE
) 
{
	out = data
	out[] = NA

	for( i in 1:nrow(data) ) {
		x = coredata(data[i,])
		o = sort.list(x, na.last = TRUE, decreasing = dirMaxMin)
		index = which(!is.na(x))
		x[] = NA

		if(len(index)>0) {
			n = min(topn, len(index))
			x[o[1:n]] = 1

			# keepn logic
			if( i>=2 ) {
				y = coredata(out[(i-1),])	# previous period selection
				n1 = min(keepn, len(index))
				y[-o[1:n1]] = NA	# remove all not in top keepn

				index1 = which(!is.na(y))
				if(len(index1)>0) {
					x[] = NA
					x[index1] = 1	# keep old selection

					for( j in 1:n ) {
						if( sum(x, na.rm = T) == topn ) break
						x[o[j]] = 1
					}
				}
			}
		}		
		out[i,] = x/sum(x, na.rm = T)	
	}
	out[is.na(out)] = 0	
	return( out )
}

```

现在我们准备使用系统性投资者工具箱中的回测库来实现这个策略：

```

# Load Systematic Investor Toolbox (SIT)
setInternet2(TRUE)
con = gzcon(url('https://github.com/systematicinvestor/SIT/raw/master/sit.gz', 'rb'))
	source(con)
close(con)

	#*****************************************************************
	# Load historical data
	#****************************************************************** 
	load.packages('quantmod')	
	tickers = spl('XLY,XLP,XLE,XLF,XLV,XLI,XLB,XLK,XLU,IWB,IWD,IWF,IWM,IWN,IWO,IWP,IWR,IWS,IWV,IWW,IWZ')	

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1970-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)
	bt.prep(data, align='keep.all', dates='1970::2011')

	#*****************************************************************
	# Code Strategies
	#****************************************************************** 
	prices = data$prices  
	n = len(tickers)  

	# find month ends
	month.ends = endpoints(prices, 'months')
		month.ends = month.ends[month.ends > 0]		

	# Equal Weight
	data$weight[] = NA
		data$weight[month.ends,] = ntop(prices, n)[month.ends,]	
		capital = 100000
		data$weight[] = (capital / prices) * data$weight
	equal.weight = bt.run(data, type='share')

	# Rank on 6 month return
	position.score = prices / mlag(prices, 126)	

	# Select Top 2 funds
	data$weight[] = NA
		data$weight[month.ends,] = ntop(position.score[month.ends,], 2)	
		capital = 100000
		data$weight[] = (capital / prices) * bt.exrem(data$weight)		
	top2 = bt.run(data, type='share', trade.summary=T)

	# Seletop Top 2 funds,  and Keep then till they are in 1:6 rank
	data$weight[] = NA
		data$weight[month.ends,] = ntop.keep(position.score[month.ends,], 2, 6)	
		capital = 100000
		data$weight[] = (capital / prices) * bt.exrem(data$weight)		
	top2.keep6 = bt.run(data, type='share', trade.summary=T)

	#*****************************************************************
	# Create Report
	#****************************************************************** 
	plotbt.custom.report(top2.keep6, top2, equal.weight, trade.summary=T)

```

请点击[此处](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot1-small.png)查看图表。

请点击[此处](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot2-small.png)查看图表。

请点击[此处](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/12/plot3-small.png)查看图表。

还有许多方法可以改进这个策略。以下是一些建议的附加方法：

唯一的限制就是你的想象力。我还会建议你在策略开发过程中进行敏感性分析，以确保你没有过度拟合数据。

要查看此例的完整源代码，请查看 GitHub 上的 [bt.rotational.trading.test() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。

更多关于示例，请查看 [M. Faber](http://www.mebanefaber.com/timing-model/) 在 [bt.timing.model.test() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)中呈现的定时模型实现，该函数位于 GitHub 上的 bt.test.r。
