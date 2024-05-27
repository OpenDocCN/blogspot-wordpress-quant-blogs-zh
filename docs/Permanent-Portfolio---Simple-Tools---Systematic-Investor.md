<!--yml

类别：未分类

日期：2024-05-18 14:36:57

-->

# 永久组合 – 简单工具 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/10/05/permanent-portfolio-simple-tools/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/10/05/permanent-portfolio-simple-tools/#0001-01-01)

我之前已经描述并对[永久组合](https://systematicinvestor.wordpress.com/2012/09/18/permanent-portfolio/)策略进行了回溯测试，基于[GestaltU](http://gestaltu.blogspot.ca/)博客中的一系列帖子。今天我想展示如何使用以下简单工具改进[永久组合](https://systematicinvestor.wordpress.com/2012/09/18/permanent-portfolio/)策略的表现：

+   波动率目标

+   风险分配

+   战略市场过滤器

首先，让我们加载股票（SPY）、黄金（GLD）、国债（TLT）和现金（SHY）的历史价格，并使用[系统投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)创建一个季度重新平衡的[永久组合](https://systematicinvestor.wordpress.com/2012/09/18/permanent-portfolio/)策略。

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
	tickers = spl('SPY,TLT,GLD,SHY')

	data <- new.env()
	getSymbols(tickers, src = 'yahoo', from = '1980-01-01', env = data, auto.assign = T)
		for(i in ls(data)) data[[i]] = adjustOHLC(data[[i]], use.Adjusted=T)

		# extend GLD with Gold.PM - London Gold afternoon fixing prices
		data$GLD = extend.GLD(data$GLD)

	bt.prep(data, align='remove.na')

	#*****************************************************************
	# Setup
	#****************************************************************** 		
	prices = data$prices   
		n = ncol(prices)

	period.ends = endpoints(prices, 'quarters')
		period.ends = period.ends[period.ends > 0]		
		period.ends = c(1, period.ends)

	models = list()

	#*****************************************************************
	# Dollar Weighted
	#****************************************************************** 			
	target.allocation = matrix(rep(1/n,n), nrow=1)
	weight.dollar = ntop(prices, n)

	data$weight[] = NA
		data$weight[period.ends,] = weight.dollar[period.ends,]
	models$dollar = bt.run.share(data, clean.signal=F)

```

现在让我们创建一个目标为 7% 年波动率的[永久组合](https://systematicinvestor.wordpress.com/2012/09/18/permanent-portfolio/)策略，基于 21 天的回溯期。

```

	#*****************************************************************
	# Dollar Weighted + 7% target volatility
	#****************************************************************** 				
	data$weight[] = NA
		data$weight[period.ends,] = target.vol.strategy(models$dollar,
						weight.dollar, 7/100, 21, 100/100)[period.ends,]
	models$dollar.target7 = bt.run.share(data, clean.signal=F)

```

请注意，将等额的美元分配给每项投资会增加风险分配给风险资产。如果我们想要在所有资产之间平均分配风险预算，我们可以考虑基于等风险分配而不是等资本（美元）分配的投资组合。

```

	#*****************************************************************
	# Risk Weighted
	#****************************************************************** 				
	ret.log = bt.apply.matrix(prices, ROC, type='continuous')
	hist.vol = sqrt(252) * bt.apply.matrix(ret.log, runSD, n = 21)	
	weight.risk = weight.dollar / hist.vol
		weight.risk = weight.risk / rowSums(weight.risk)

	data$weight[] = NA
		data$weight[period.ends,] = weight.risk[period.ends,]
	models$risk = bt.run.share(data, clean.signal=F)

```

我们也可以使用市场过滤器，例如 10 个月移动平均线，来控制投资组合的回撤。

```

	#*****************************************************************
	# Market Filter (tactical): 10 month moving average
	#****************************************************************** 				
	period.ends = endpoints(prices, 'months')
		period.ends = period.ends[period.ends > 0]		
		period.ends = c(1, period.ends)

	sma = bt.apply.matrix(prices, SMA, 200)
	weight.dollar.tactical = weight.dollar * (prices > sma)	

	data$weight[] = NA
		data$weight[period.ends,] = weight.dollar.tactical[period.ends,]
	models$dollar.tactical = bt.run.share(data, clean.signal=F)

```

最后，让我们结合市场过滤和波动率目标：

```

	#*****************************************************************
	# Tactical + 7% target volatility
	#****************************************************************** 				
	data$weight[] = NA
		data$weight[period.ends,] = target.vol.strategy(models$dollar.tactical,
						weight.dollar.tactical, 7/100, 21, 100/100)[period.ends,]
	models$dollar.tactical.target7 = bt.run.share(data, clean.signal=F)

	#*****************************************************************
	# Create Report
	#******************************************************************       
	plotbt.custom.report.part1(models)       

	plotbt.strategy.sidebyside(models)	

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/10/plot1-small.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/10/plot2-small.png)

结合市场过滤和波动率目标的最终投资组合比原始的[永久组合](https://systematicinvestor.wordpress.com/2012/09/18/permanent-portfolio/)策略要好得多：收益稍微下降，但回撤减少了一半。

要查看此示例的完整源代码，请查看[GitHub 上的 bt.test.r 中的 bt.permanent.portfolio2.test() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
