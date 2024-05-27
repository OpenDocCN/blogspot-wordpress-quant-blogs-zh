<!--yml

类别：未分类

日期：2024-05-18 14:48:46

-->

# 资产配置简介 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2011/10/13/introduction-to-asset-allocation/#0001-01-01`](https://systematicinvestor.wordpress.com/2011/10/13/introduction-to-asset-allocation/#0001-01-01)

这是关于[资产配置](http://en.wikipedia.org/wiki/Asset_allocation)、风险度量与投资组合构建的一系列文章中的第一篇。我在所有文章中都会使用简单且原始的历史输入假设来进行说明。

在这些系列中，我计划讨论：

本篇文章的计划是介绍资产配置。我将展示如何创建和可视化输入假设，设置约束，并创建[马科维茨均值-方差有效前沿](http://en.wikipedia.org/wiki/Efficient_frontier)。

首先让我们加载[系统投资者工具箱](https://github.com/systematicinvestor/SIT)并从[雅虎财经](http://finance.yahoo.com/)下载历史价格数据：

```

# load Systematic Investor Toolbox
setInternet2(TRUE)
source(gzcon(url('https://github.com/systematicinvestor/SIT/raw/master/sit.gz', 'rb')))

load.packages('quantmod')

# load historical prices from Yahoo Finance
symbols = spl('SPY,QQQ,EEM,IWM,EFA,TLT,IYR,GLD')
symbol.names = spl('S&P 500,Nasdaq 100,Emerging Markets,Russell 2000,EAFE,20 Year
Treasury,U.S. Real Estate,Gold')

getSymbols(symbols, from = '1980-01-01', auto.assign = TRUE)

# align dates for all symbols & convert to monthly
hist.prices = merge(SPY,QQQ,EEM,IWM,EFA,TLT,IYR,GLD)
	month.ends = endpoints(hist.prices, 'months')
	hist.prices = Cl(hist.prices)[month.ends, ]
	colnames(hist.prices) = symbols

# remove any missing data
hist.prices = na.omit(hist.prices['1995::2010'])

# compute simple returns
hist.returns = na.omit( ROC(hist.prices, type = 'discrete') )

```

为了创建输入假设，我将使用历史月收益率计算平均值、标准差和皮尔逊相关系数：

```

# compute historical returns, risk, and correlation
ia = list()
ia$expected.return = apply(hist.returns, 2, mean, na.rm = T)
ia$risk = apply(hist.returns, 2, sd, na.rm = T)
ia$correlation = cor(hist.returns, use = 'complete.obs', method = 'pearson')

ia$symbols = symbols
ia$symbol.names = symbol.names
ia$n = len(symbols)
ia$hist.returns = hist.returns

# convert to annual, year = 12 months
annual.factor = 12
ia$expected.return = annual.factor * ia$expected.return
ia$risk = sqrt(annual.factor) * ia$risk

# compute covariance matrix
ia$risk = iif(ia$risk == 0, 0.000001, ia$risk)
ia$cov = ia$cor * (ia$risk %*% t(ia$risk))

```

现在是一个很好的时机来可视化输入假设：

```

# visualize input assumptions
plot.ia(ia)

# display each asset in the Risk - Return plot
layout(1)
par(mar = c(4,4,2,1), cex = 0.8)
x = 100 * ia$risk
y = 100 * ia$expected.return

plot(x, y, xlim = range(c(0, x)), ylim = range(c(0, y)),
	xlab='Risk', ylab='Return', main='Risk vs Return', col='black')
grid();
text(x, y, symbols,	col = 'blue', adj = c(1,1), cex = 0.8)

```

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/10/plot1-small3.png)

![plot2.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/10/plot2-small3.png)

这些输入假设存在许多问题，例如：

+   历史平均值可能不是一个好的预期回报的代理

+   加权历史平均值可能是一个更好的选择，因为它给最近观察到的数据赋予了更大的权重

+   相关性并不稳定

+   波动性倾向于聚集

+   对于现金和债券的输入假设，用当前收益率和短期波动性来近似会更好

我只使用这些简单且原始的历史输入假设作为说明。

为了创建[有效前沿](http://en.wikipedia.org/wiki/Efficient_frontier)，我将考虑分配到任何资产类别的投资组合，其分配范围在 0%到 80%之间，且投资组合的总权重等于 100%。（我只是作为一个例子，将任何资产类别的最大分配限制在 80%）

```

# Create Efficient Frontier
n = ia$n

# 0 <= x.i <= 0.8 
constraints = new.constraints(n, lb = 0, ub = 0.8)

# SUM x.i = 1 ( total portfolio weight = 100%)
constraints = add.constraints(rep(1, n), 1, type = '=', constraints)

# create efficient frontier consisting of 50 portfolios
ef = portopt(ia, constraints, 50, 'Sample Efficient Frontier')

# plot efficient frontier
plot.ef(ia, list(ef))

```

![plot3.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/10/plot3-small2.png)

过渡图显示了我们在有效前沿上移动时的组合权重。我在 X 轴上显示组合风险，在 Y 轴上显示组合权重。切片宽度代表给定风险水平下的组合权重。例如，在上面的过渡图图中，黄金（GLD - 灰色）在较低风险水平时的分配约为 20%，并且逐渐增加到较高风险水平时的 80%。同样，债券（TLT - 粉色）在较低风险水平时的分配约为 50%，并且逐渐减少到较高风险水平时的 0%。

最后，我想讲解一下“portopt”函数的逻辑，这个函数为我们创建有效前沿。创建有效前沿的第一步是找到顶部、右侧（最大回报组合）和底部、左侧（最小风险组合）。接下来，我将最小风险组合和最大回报组合之间的回报空间分为 n 个组合，这些组合在等距点上。对于每个点，我找到一个最小风险组合，并增加一个约束条件，即组合回报必须等于该点的目标回报。最后一步是计算有效前沿上组合的回报和风险。

```

portopt <- function
(
	ia,				# Input Assumptions
	constraints = NULL,		# Constraints
	nportfolios = 50,		# Number of portfolios
	name = 'Risk',			# Name
	min.risk.fn = min.risk.portfolio	# Risk Measure
)
{
	# set up output 
	out = list(weight = matrix(NA, nportfolios, ia$n))
		colnames(out$weight) = ia$symbols		

	# find maximum return portfolio	
	out$weight[1, ] = max.return.portfolio(ia, constraints)

	# find minimum risk portfolio
	out$weight[nportfolios, ] = match.fun(min.risk.fn)(ia, constraints)	

	# find points on efficient frontier
	out$return = portfolio.return(out$weight, ia)
	target = seq(out$return[1], out$return[nportfolios], length.out = nportfolios)

	constraints = add.constraints(ia$expected.return, target[1], type = '=', constraints)

	for(i in 2:(nportfolios - 1) ) {
		constraints$b[1] = target[i]
		out$weight[i, ] = match.fun(min.risk.fn)(ia, constraints)
	}

	# compute risk / return
	out$return = portfolio.return(out$weight, ia)
	out$risk = portfolio.risk(out$weight, ia)
	out$name = name

	return(out)			
}

```

在下一篇文章中，我将讨论最大损失风险度量，并将其与传统的风险度量进行比较，这种传统风险度量是通过标准差来衡量的。

要查看这个示例的完整源代码，请查看[aa.test()函数在 github 上的 aa.test.r 文件](https://github.com/systematicinvestor/SIT/blob/master/R/aa.test.r)。
