<!--yml

分类：未分类

日期：2024-05-18 14:42:39

-->

# 多因子模型 – 构建风险模型 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/02/21/multiple-factor-model-building-risk-model/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/02/21/multiple-factor-model-building-risk-model/#0001-01-01)

这是关于多因子模型的系列文章的第四篇。我将在前一篇帖子[多因子模型 – 构建 CSFB 因子](https://systematicinvestor.wordpress.com/2012/02/13/multiple-factor-model-building-csfb-factors/)中展示的代码基础上构建一个多因子风险模型。有关多因子风险模型的示例，请阅读以下参考资料：

本帖大纲：

+   运行横截面回归以估计因子回报

+   使用收缩估计器计算因子协方差

+   使用 GARCH(1,1)预测股票特定方差

+   使用多因子模型计算投资组合风险，并与投资组合回报的历史标准差进行比较。

首先，我们加载在[前一篇帖子](https://systematicinvestor.wordpress.com/2012/02/13/multiple-factor-model-building-csfb-factors/)末尾保存的瑞士信贷银行（CSFB）因子。[如果你缺少 data.factors.Rdata 文件，请首先执行 fm.all.factor.test()函数以创建并保存 CSFB 因子。]接下来，我将运行横截面回归来估计因子回报。

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)
# https://systematicinvestor.wordpress.com/systematic-investor-toolbox/
###############################################################################
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)
	#*****************************************************************
	# Load factor data that we saved at the end of the fm.all.factor.test functions
	#****************************************************************** 
	load.packages('quantmod,abind')	

	load(file='data.factors.Rdata')
		# remove Composite Average factor
		factors.avg = factors.avg[which(names(factors.avg) != 'AVG')]	

	#*****************************************************************
	# Run cross sectional regression to estimate factor returns
	#****************************************************************** 
	nperiods = nrow(next.month.ret)
	n = ncol(next.month.ret)

	# create sector dummy variables: binary 0/1 values for each sector
	nsectors = len(levels(sectors))	
	sectors.matrix = array(double(), c(nperiods, n, nsectors))
		dimnames(sectors.matrix)[[3]] = levels(sectors)		
	for(j in levels(sectors)) {
		sectors.matrix[,,j] = matrix(sectors == j,  nr=nperiods, nc=n, byrow=T)
	}

	# create matrix for each factor
	factors.matrix = abind(factors.avg, along = 3)		

	# combine sector dummies and all factors
	all.data = abind(sectors.matrix, factors.matrix)		

	# create betas and specific.return
	beta = all.data[,1,] * NA
	specific.return = next.month.ret * NA
		nfactors = ncol(beta)

	# append next.month.ret to all.data			
	all.data = abind(next.month.ret, all.data, along = 3)
		dimnames(all.data)[[3]][1] = 'Ret'

	# estimate betas (factor returns)
	for(t in 12:(nperiods-1)) {		
		temp = all.data[t:t,,]
		x = temp[,-c(1:2)]
		y = temp[,1]
		b = lm(y~x)$coefficients

		b[2:nsectors] = b[1] + b[2:nsectors]
		beta[(t+1),] = b		

		specific.return[(t+1),] = y - rowSums(temp[,-1] * matrix(b, n, nfactors, byrow=T), na.rm=T)	
	}

```

为了估计因子回报（贝塔值），我们求解以下多因子模型的系数：

```

Ret = b1 * F1 + b2 * F2 + ... + bn * Fn + e
where 
b1...bn are estimated factor returns
F1...Fn are factor exposures. I.e. sector dummies and CSFB factor exposures
e is stock specific return, not captured by factors F1...Fn
```

请注意，我们不能在回归中包含第一个行业虚拟变量，否则我们会得到第一个行业虚拟变量与其他所有行业虚拟变量之间的线性依赖关系。第一个行业虚拟变量的行业效应被吸收在回归的截距中。

估计这个回归有几种不同的方法。例如，可以使用以下代码估计稳健线性模型：

```

	load.packages('MASS')
	temp = rlm(y~x)$coefficients

```

quantile 回归可以通过以下代码估计：

```

	load.packages('quantreg')
	temp = rq(y ~ x, tau = 0.5)$coefficients

```

接下来，让我们看看累计因子回报。

```

	#*****************************************************************
	# helper function
	#****************************************************************** 	
	fm.hist.plot <- function(temp, smain=NULL) {			
		ntemp = ncol(temp)		
		cols = plota.colors(ntemp)	
		plota(temp, ylim = range(temp), log='y', main=smain)
		for(i in 1:ntemp) plota.lines(temp[,i], col=cols[i])
		plota.legend(colnames(temp), cols, as.list(temp))
	}

	#*****************************************************************
	# Examine historical cumulative factor returns
	#****************************************************************** 	
	temp = make.xts(beta, index(next.month.ret))
		temp = temp['2000::',]
		temp[] = apply(coredata(temp), 2, function(x) cumprod(1 + ifna(x,0)))

	fm.hist.plot(temp[,-c(1:nsectors)], 'Factor Returns')

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/02/plot1-small2.png)

价格反转（PR）和小市值（SS）因子表现良好。

接下来，让我们估计滚动 24 个月窗口期的因子协方差矩阵。

```

	load.packages('BurStFin')	
	factor.covariance = array(double(), c(nperiods, nfactors, nfactors))
		dimnames(factor.covariance)[[2]] = colnames(beta)
		dimnames(factor.covariance)[[3]] = colnames(beta)

	# estimate factor covariance
	for(t in 36:nperiods) {
		factor.covariance[t,,] = var.shrink.eqcor(beta[(t-23):t,])
	}

```

接下来，让我们使用 GARCH(1,1)预测股票特定方差。我将使用[利用 Garch 波动率预测交易](https://systematicinvestor.wordpress.com/2012/01/06/trading-using-garch-volatility-forecast/)帖子中描述的 GARCH 估计程序。

```

	#*****************************************************************
	# Compute stocks specific variance foreasts using GARCH(1,1)
	#****************************************************************** 	
	load.packages('tseries,fGarch')	

	specific.variance = next.month.ret * NA

	for(i in 1:n) {
		specific.variance[,i] = bt.forecast.garch.volatility(specific.return[,i], 24) 
	}

	# compute historical specific.variance
	hist.specific.variance = next.month.ret * NA
	for(i in 1:n) hist.specific.variance[,i] = runSD(specific.return[,i], 24)	

	# if specific.variance is missing use historical specific.variance
	specific.variance[] = ifna(coredata(specific.variance), coredata(hist.specific.variance))	

	#*****************************************************************
	# Save multiple factor risk model to be used later during portfolio construction
	#****************************************************************** 
	save(all.data, factor.covariance, specific.variance, file='risk.model.Rdata')

```

现在我们有了计算投资组合风险的所有要素：

```

Portfolio Risk = (common factor variance + specific variance)⁰.5
	common factor variance = (portfolio factor exposure) * factor covariance matrix * (portfolio factor exposure)'
	specific variance = (specific.variance)² * (portfolio weights)²
```

```

	#*****************************************************************
	# Compute portfolio risk
	#****************************************************************** 
	portfolio = rep(1/n, n)
		portfolio = matrix(portfolio, n, nfactors)

	portfolio.risk = next.month.ret[,1] * NA
	for(t in 36:(nperiods-1)) {	
		portfolio.exposure = colSums(portfolio * all.data[t,,-1], na.rm=T)

		portfolio.risk[t] = sqrt(
			portfolio.exposure %*% factor.covariance[t,,] %*% (portfolio.exposure) + 
			sum(specific.variance[t,]² * portfolio[,1]², na.rm=T)
			)
	}

```

接下来，让我们比较使用多因子风险模型估计的投资组合风险与投资组合历史风险。

```

	#*****************************************************************
	# Compute historical portfolio risk
	#****************************************************************** 
	portfolio = rep(1/n, n)
		portfolio = t(matrix(portfolio, n, nperiods))

	portfolio.returns = next.month.ret[,1] * NA
		portfolio.returns[] = rowSums(mlag(next.month.ret) * portfolio, na.rm=T)

	hist.portfolio.risk = runSD(portfolio.returns, 24)

	#*****************************************************************
	# Plot risks
	#****************************************************************** 			
	plota(portfolio.risk['2000::',], type='l')
		plota.lines(hist.portfolio.risk, col='blue')
		plota.legend('Risk,Historical Risk', 'black,blue')

```

![plot2.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/02/plot2-small3.png)

多因子风险模型在大多数时间都能较好地估计投资组合风险。

要查看此示例的完整源代码，请查看[github 上 factor.model.test.r 文件中的 fm.risk.model.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/factor.model.test.r)。
