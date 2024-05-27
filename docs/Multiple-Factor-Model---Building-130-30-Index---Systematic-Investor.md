<!--yml

分类：未分类

日期：2024-05-18 14:42:22

-->

# 多因子模型 – 构建 130/30 指数 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/03/06/multiple-factor-model-building-13030-index/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/03/06/multiple-factor-model-building-13030-index/#0001-01-01)

尼科（Nico）在他的评论中向我推荐了[A. Lo, P. Patel](http://math.nyu.edu/faculty/avellane/Lo13030.pdf)的论文[130/30: The New Long-Only (2008)](http://math.nyu.edu/faculty/avellane/Lo13030.pdf)，这篇论文在[多因子模型 – 构建 CSFB 因子](https://systematicinvestor.wordpress.com/2012/02/13/multiple-factor-model-building-csfb-factors/)一文中提及。该论文提供了一个非常详细的步骤指南，用于使用平均 CSFB 因子作为 alpha 模型和[MSCI Barra 多因子风险模型](http://www.alacra.com/alacra/help/barra_handbook_US.pdf)构建 130/30 指数。今天，我想采用这种方法，并展示如何根据我们在[多因子模型 – 构建 CSFB 因子](https://systematicinvestor.wordpress.com/2012/02/13/multiple-factor-model-building-csfb-factors/)和[多因子模型 – 构建风险模型](https://systematicinvestor.wordpress.com/2012/02/21/multiple-factor-model-building-risk-model/)文章中创建的 CSFB 因子和风险模型构建 130/30 指数。

首先，让我们加载保存于[多因子模型 – 构建 CSFB 因子](https://systematicinvestor.wordpress.com/2012/02/13/multiple-factor-model-building-csfb-factors/)一文末尾的 CSFB 因子数据。如果你丢失了`data.factors.Rdata`文件，请先执行`fm.all.factor.test()`函数来创建并保存 CSFB 因子。[接下来，让我们加载在[多因子模型 – 构建风险模型](https://systematicinvestor.wordpress.com/2012/02/21/multiple-factor-model-building-risk-model/)一文末尾保存的多因子风险模型。如果你丢失了`risk.model.Rdata`文件，请先执行`fm.risk.model.test()`函数来创建并保存多因子风险模型。]接下来，我将计算一个两年滚动窗口内的贝塔值。

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)
# https://systematicinvestor.wordpress.com/systematic-investor-toolbox/
###############################################################################
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

	#*****************************************************************
	# Load data
	#****************************************************************** 
	load.packages('quantmod')	

	# Load CSFB factor data that we saved at the end of the fm.all.factor.test function
	load(file='data.factors.Rdata')
		nperiods = nrow(next.month.ret)
		tickers = colnames(next.month.ret)
		n = len(tickers)

	# Load multiple factor risk model data that we saved at the end of the fm.risk.model.test function	
	load(file='risk.model.Rdata')
		factor.exposures = all.data[,,-1]	
		factor.names = dimnames(factor.exposures)[[3]]
		nfactors = len(factor.names)

	#*****************************************************************
	# Compute Betas: b = cov(r,m) / var(m)
	# The betas are measured on a two-year rolling window
	# http://en.wikipedia.org/wiki/Beta_(finance)
	#****************************************************************** 
	ret = mlag(next.month.ret)
	beta = ret * NA

	# 1/n benchmark portfolio
	benchmark = ntop(ret, n)	
	benchmark.ret = rowSums(benchmark * ret, na.rm=T)

	# estimate betas
	for(t in 24:nperiods) {
		t.index = (t-23):t
		benchmark.var = var( benchmark.ret[t.index], na.rm=T )

		t.count = count(ret[t.index, ])
		t.cov = cov( ifna(ret[t.index,], 0), benchmark.ret[t.index], use='complete.obs' )

		# require at least 20 months of history
		beta[t,] = iif(t.count > 20, t.cov/benchmark.var, NA)
	}

```

为了每月构建有效组合，我将解决如下形式的均值-方差组合优化问题：

```
Max weight * return - risk.aversion * weight * Covariance * weight 
Sum weight = 1
Sum weight * beta = 1
0 <= weight <= 0.1
```

请阅读 S. Liu, R. Xu 在[风险厌恶对优化影响](http://www.mscibarra.com/research/articles/2010/The%20Effects%20of%20Risk%20Aversion%20on%20Optimization%20(Feb%202010).pdf)论文中对此优化问题的详细讨论。

请注意，我将使用风险厌恶系数`risk.aversion = 0.0075`和组合贝塔=1，如[A. Lo, P. Patel](http://math.nyu.edu/faculty/avellane/Lo13030.pdf)在论文[130/30: The New Long-Only (2008)](http://math.nyu.edu/faculty/avellane/Lo13030.pdf)第 22 页所讨论的。为了建模组合贝塔约束，我将使用这样一个事实：[组合贝塔等于个别资产贝塔的加权平均](http://www.duke.edu/~charvey/Classes/ba350/riskman/riskman.htm)。

```

	#*****************************************************************
	# Construct LONG ONLY portfolio using the multiple factor risk model
	#****************************************************************** 
	load.packages('quadprog,corpcor,kernlab')

	weight = NA * next.month.ret
	weights = list()
		weights$benchmark = ntop(beta, n)		
		weights$long.alpha = weight

	for(t in 36:nperiods) {	
		#--------------------------------------------------------------------------
		# Create constraints
		#--------------------------------------------------------------------------
		# set min/max wgts for individual stocks: 0 =< x <= 10/100
		constraints = new.constraints(n, lb = 0, ub = 10/100)

		# wgts must sum to 1 (fully invested)
		constraints = add.constraints(rep(1,n), type = '=', b = 1, constraints)

		#--------------------------------------------------------------------------
		# beta of portfolio is the weighted average of the individual asset betas		
		# http://www.duke.edu/~charvey/Classes/ba350/riskman/riskman.htm
		#--------------------------------------------------------------------------
		constraints = add.constraints(ifna(as.vector(beta[t,]),0), type = '=', b = 1, constraints)

		#--------------------------------------------------------------------------
		# Create factor exposures constraints
		#--------------------------------------------------------------------------	
		# adjust prior constraints, add factor exposures
		constraints = add.variables(nfactors, constraints)

		# BX - X1 = 0
		constraints = add.constraints(rbind(ifna(factor.exposures[t,,], 0), -diag(nfactors)), rep(0, nfactors), type = '=', constraints)

		#--------------------------------------------------------------------------
		# Create Covariance matrix
		# [Qu  0]
		# [ 0 Qf]
		#--------------------------------------------------------------------------
		temp = diag(n)
			diag(temp) = ifna(specific.variance[t,], mean(coredata(specific.variance[t,]), na.rm=T))²
		cov.temp = diag(n + nfactors)
			cov.temp[1:n,1:n] = temp
		cov.temp[(n+1):(n+nfactors),(n+1):(n+nfactors)] = factor.covariance[t,,]

		#--------------------------------------------------------------------------
		# create input assumptions
		#--------------------------------------------------------------------------
		ia = list()	
		ia$n = nrow(cov.temp)
		ia$annual.factor = 12

		ia$symbols = c(tickers, factor.names)

		ia$cov = cov.temp	

		#--------------------------------------------------------------------------
		# page 9, Risk: We use the Barra default setting, risk aversion value of 0.0075, and
		# AS-CF risk aversion ratio of 1.
		#
		# The Effects of Risk Aversion on Optimization (2010) by S. Liu, R. Xu
		# page 4/5
		#--------------------------------------------------------------------------
		risk.aversion = 0.0075
		ia$cov.temp = ia$cov	

		# set expected return
		alpha = factors.avg$AVG[t,] / 5
		ia$expected.return = c(ifna(coredata(alpha),0), rep(0, nfactors))

		# remove companies that have no beta from optimization
		index = which(is.na(beta[t,]))
		if( len(index) > 0) {
			constraints$ub[index] = 0
			constraints$lb[index] = 0
		}

		# find solution
		sol = solve.QP.bounds(Dmat = 2* risk.aversion * ia$cov.temp, dvec = ia$expected.return, 
					Amat = constraints$A, bvec = constraints$b, 
					meq = constraints$meq, lb = constraints$lb, ub = constraints$ub)

		weights$long.alpha[t,] = sol$solution[1:n]
	}

```

接下来，让我们构建一个 130/30 投资组合。我将限制投资组合权重为±10%，并将使用我在[130/30 投资组合构建](https://systematicinvestor.wordpress.com/2011/10/18/13030-porfolio-construction/)文章中记录的投资组合构建技术。

```

	#*****************************************************************
	# Construct Long/Short 130:30 portfolio using the multiple factor risk model
	# based on the examples in the aa.long.short.test functions
	#****************************************************************** 
	weights$long.short.alpha = weight

	for(t in 36:nperiods) {	
		#--------------------------------------------------------------------------
		# Create constraints
		#--------------------------------------------------------------------------
		# set min/max wgts for individual stocks: -10/100 =< x <= 10/100
		constraints = new.constraints(n, lb = -10/100, ub = 10/100)

		# wgts must sum to 1 (fully invested)
		constraints = add.constraints(rep(1,n), type = '=', b = 1, constraints)

		#--------------------------------------------------------------------------
		# beta of portfolio is the weighted average of the individual asset betas		
		# http://www.duke.edu/~charvey/Classes/ba350/riskman/riskman.htm
		#--------------------------------------------------------------------------
		constraints = add.constraints(ifna(as.vector(beta[t,]),0), type = '=', b = 1, constraints)

		#--------------------------------------------------------------------------
		# Create factor exposures constraints
		#--------------------------------------------------------------------------	
		# adjust prior constraints, add factor exposures
		constraints = add.variables(nfactors, constraints)

		# BX - X1 = 0
		constraints = add.constraints(rbind(ifna(factor.exposures[t,,], 0), -diag(nfactors)), rep(0, nfactors), type = '=', constraints)

		#--------------------------------------------------------------------------
		# Create 130:30
		# -v.i <= x.i <= v.i, v.i>0, SUM(v.i) = 1.6
		#--------------------------------------------------------------------------		
		# adjust prior constraints, add v.i
		constraints = add.variables(n, constraints)

		# -v.i <= x.i <= v.i
		#   x.i + v.i >= 0
		constraints = add.constraints(rbind(diag(n), matrix(0,nfactors,n)  ,diag(n)), rep(0, n), type = '>=', constraints)
		#   x.i - v.i <= 0
		constraints = add.constraints(rbind(diag(n), matrix(0,nfactors,n), -diag(n)), rep(0, n), type = '<=', constraints)

		# SUM(v.i) = 1.6
		constraints = add.constraints(c(rep(0, n), rep(0, nfactors), rep(1, n)), 1.6, type = '=', constraints)

		#--------------------------------------------------------------------------
		# Create Covariance matrix
		# [Qu  0]
		# [ 0 Qf]
		#--------------------------------------------------------------------------
		temp = diag(n)
			diag(temp) = ifna(specific.variance[t,], mean(coredata(specific.variance[t,]), na.rm=T))²
		cov.temp = 0*diag(n + nfactors + n)
			cov.temp[1:n,1:n] = temp
		cov.temp[(n+1):(n+nfactors),(n+1):(n+nfactors)] = factor.covariance[t,,]

		#--------------------------------------------------------------------------
		# create input assumptions
		#--------------------------------------------------------------------------
		ia = list()	
		ia$n = nrow(cov.temp)
		ia$annual.factor = 12

		ia$symbols = c(tickers, factor.names, tickers)

		ia$cov = cov.temp	

		#--------------------------------------------------------------------------
		# page 9, Risk: We use the Barra default setting, risk aversion value of 0.0075, and
		# AS-CF risk aversion ratio of 1.
		#
		# The Effects of Risk Aversion on Optimization (2010) by S. Liu, R. Xu
		# page 4/5
		#--------------------------------------------------------------------------
		risk.aversion = 0.0075
		ia$cov.temp = ia$cov

		# set expected return
		alpha = factors.avg$AVG[t,] / 5
		ia$expected.return = c(ifna(coredata(alpha),0), rep(0, nfactors), rep(0, n))

		# remove companies that have no beta from optimization
		index = which(is.na(beta[t,]))
		if( len(index) > 0) {
			constraints$ub[index] = 0
			constraints$lb[index] = 0
		}

		# find solution
		sol = solve.QP.bounds(Dmat = 2* risk.aversion * ia$cov.temp, dvec = ia$expected.return, 
					Amat = constraints$A, bvec = constraints$b, 
					meq = constraints$meq, lb = constraints$lb, ub = constraints$ub)

		weights$long.short.alpha[t,] = sol$solution[1:n]
	}

```

在此阶段，我们创建了月度的只做多和 130:30 投资组合。让我们来查看它们的状态转换图。

```

	#*****************************************************************
	# Plot Transition Maps
	#****************************************************************** 	
	layout(1:3)
	for(i in names(weights)) plotbt.transition.map(weights[[i]], i)

```

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/03/plot1-small.png)

只做多投资组合（long.alpha）的权重之和为 100%，而 130:30 投资组合（long.short.alpha）的权重为 130%做多和 30%做空，符合预期。

接下来，让我们基于这些投资组合创建交易策略并检查它们的表现。

```

	#*****************************************************************
	# Create strategies
	#****************************************************************** 	
	prices = data$prices
		prices = bt.apply.matrix(prices, function(x) ifna.prev(x))

	# find month ends
	month.ends = endpoints(prices, 'months')

	# create strategies that invest in each qutile
	models = list()

	for(i in names(weights)) {
		data$weight[] = NA
			data$weight[month.ends,] = weights[[i]]
			capital = 100000
			data$weight[] = (capital / prices) * (data$weight)	
		models[[i]] = bt.run(data, type='share', capital=capital)
	}

	#*****************************************************************
	# Create Report
	#****************************************************************** 	
	models = rev(models)

	plotbt.custom.report.part1(models, dates='1998::')
	plotbt.custom.report.part2(models)

```

![plot2.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/03/plot2-small.png)

![plot3.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/03/plot3-small.png)

130:30 投资组合表现最佳，相比只做多（long-only）和基准（1/N）投资组合，它能带来更高的回报，且回撤更小。

注意事项：上述结果基于$0 交易费用（即交易免费）。此外，我使用了整个历史期间的道琼斯指数成分股；因此，引入了[幸存者偏差](http://www.investopedia.com/terms/s/survivorshipbias.asp)（即道琼斯指数在过去的 20 年中改变了其构成几次）。

让我们来看看假设交易费用为$0 的问题影响有多大，让我们来查看一下投资组合的年换手率。

```

	# Plot Portfolio Turnover for each strategy
	layout(1)
	barplot.with.labels(sapply(models, compute.turnover, data), 'Average Annual Portfolio Turnover')

```

![plot4.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/03/plot4-small.png)

130:30 投资组合的换手率相当高；因此，它在实际操作中的表现可能不如我们在回测中的结果那样好。

要查看此例的完整源代码，请查看[fm.long.short.test()函数在 factor.model.test.r 中的代码](https://github.com/systematicinvestor/SIT/blob/master/R/factor.model.test.r)。
