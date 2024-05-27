<!--yml

类别：未分类

日期：2024-05-18 14:49:03

-->

# 风险、收益和分析师评级 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2011/10/08/risk-return-and-analyst-ratings/#0001-01-01`](https://systematicinvestor.wordpress.com/2011/10/08/risk-return-and-analyst-ratings/#0001-01-01)

今天我想讨论风险、收益和分析师评级之间的关系。让我们从定义我们的股票范围开始：从 [道琼斯工业平均指数(^DJI)](http://finance.yahoo.com/q/cp?s=%5EDJI+Components) 中选取的 30 支股票。对于每支股票，我将计算 2010 年至 2011 年的升级和降级次数、风险和收益。我将进行线性回归并计算升级和降级次数与风险和收益之间的相关性。

让我们使用 R 和[Systematic Investor Toolbox](https://github.com/systematicinvestor/SIT)来实施这个计划。

首先，让我们加载 Systematic Investor Toolbox 和[quantmod](http://www.quantmod.com/) 包

```

# load Systematic Investor Toolbox
setInternet2(TRUE)
source(gzcon(url('https://github.com/systematicinvestor/SIT/raw/master/sit.gz', 'rb')))

load.packages('quantmod,car')

```

我将从 Yahoo Finance 获取 [道琼斯工业平均指数(^DJI)](http://finance.yahoo.com/q/cp?s=%5EDJI+Components) 中的股票列表：

```

# download Dow Jones Components
url = 'http://finance.yahoo.com/q/cp?s=^DJI+Components'
txt = join(readLines(url))

# extract table from this page
temp = extract.table.from.webpage(txt, 'Symbol', hasHeader = T)

# Symbols
Symbols = temp[, 'Symbol']

```

我将从[Yahoo Finance](http://finance.yahoo.com/q/ud?s=IBM)获取每支股票的升级和降级历史记录：

```

# Matrix with number of Upgrades/Downgrades in 2010:2011
up.down.stats = matrix( NA, nrow = len(Symbols), ncol = 3 )
	rownames(up.down.stats) = Symbols
	colnames(up.down.stats) = spl('N,Return,Risk')

# Get Upgrade/Downgrade statistics and compute Risk and Return for each symbol
for( Symbol in Symbols ) {
	cat('Downloading', Symbol, '\n')

	# download Upgrade/Downgrade table
	url = paste('http://finance.yahoo.com/q/ud?s=', Symbol, sep = '')
	txt = join(readLines(url))

	# extract table from this page
	temp = extract.table.from.webpage(txt, 'Research Firm', hasHeader = T)

	# find number of Upgrades/Downgrades in 2010:2011
	event.year = format(as.Date(temp[, 'Date'], '%d-%b-%y'), '%Y')
	up.down.stats[Symbol, 'N'] = sum(event.year == '2010' | event.year == '2011')

	# download price history from Yahoo
	data = getSymbols(Symbol, from = '1980-01-01', auto.assign = FALSE)
	returns = ROC(Cl(data['2010::2011']), type = 'discrete')
		returns = na.omit(returns)

	# compute basic measures of Return and Risk
	up.down.stats[Symbol, 'Return'] = 252 * mean(returns)
	up.down.stats[Symbol, 'Risk'] = sqrt(252) * sd(returns)
}

```

让我们来看一下数据：

```

# sort up.down.stats by number of events
up.down.stats = up.down.stats[ order(up.down.stats[,'N']), , drop = FALSE]
up.down.stats[, spl('Return,Risk')] = round(100 * up.down.stats[, spl('Return,Risk')], 1)

# plot table
plot.table(up.down.stats)

# barplot of Number of Upgrades & Downgrades in 2010:2011
par(mar = c(5,4,2,1), cex = 0.8)
barplot( up.down.stats[, 'N'],
	xlab = 'Symbols', ylab = 'Number of Upgrades & Downgrades in 2010:2011',
	main = 'Upgrades & Downgrades in 2010:2011 from Yahoo Finance',
	names.arg = rownames(up.down.stats), las = 2 )

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/10/plot1-small1.png)

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/10/plot2-small1.png)

让我们运行线性回归并计算升级和降级次数与风险和收益之间的相关性：

```

# run linear regression and compute correlation between number of events and Returns / Risk
for( measure in spl('Risk,Return') ) {
	x = up.down.stats[, 'N']
	y = up.down.stats[, measure]

	# linear regression
	fit = lm(y ~ x)
	print(summary(fit))

	par(mar = c(5,4,2,1))
	plot(x, y, xlab = 'Number of of Upgrades & Downgrades', ylab = measure,
		main = paste(plota.format(100 * cor(x,y), 0, '', '%') , 'correlation between', measure, 'and Number of Events'))
		grid()
		text(x, y, rownames(up.down.stats), col = 'blue', adj = c(1,1), cex = 0.8)
		abline(coef = coef(fit), lty=2)

	# compute ellipsoid at 50% confidence level
	d = dataEllipse(x, y, levels = c(0.5), draw = FALSE)
	lines(d, col='red', lty=3)
}

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/10/plotrisk-small.png)

```
Coefficients:
            Estimate Std. Error t value Pr(>|t|)
(Intercept)  20.1766     2.3879   8.449 3.45e-09 ***
x             0.6589     0.3022   2.180   0.0378 *
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Multiple R-squared: 0.1451,     Adjusted R-squared: 0.1146
F-statistic: 4.753 on 1 and 28 DF,  p-value: 0.0378
```

升级和降级次数与风险之间存在正相关关系。线性回归中的 beta 系数为正，且在 5% 的置信水平上显著。

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/10/plotreturn-small.png)

```
Coefficients:
            Estimate Std. Error t value Pr(>|t|)
(Intercept)  14.5098     4.5533   3.187  0.00352 **
x            -1.6238     0.5763  -2.818  0.00877 **
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Multiple R-squared: 0.2209,     Adjusted R-squared: 0.1931
F-statistic:  7.94 on 1 and 28 DF,  p-value: 0.008769
```

升级和降级次数与收益之间存在负相关关系。线性回归中的 beta 系数为负，且在 1% 的置信水平上显著。

从这些观察中可以得出结论，随着升级和降级数量的增加，2010 年至 2011 年期间风险上升，收益下降。然而，我对这个分析有一些问题：

+   我们以相同的方式检查了所有股票；然而，来自不同行业的公司可能具有自然存在的不同风险/收益特征。

+   我们以相同的方式对待所有事件；然而，升级/降级/启动操作可能对公司的股票价格产生不同的影响。

请告诉我你认为我的分析还有什么问题。
