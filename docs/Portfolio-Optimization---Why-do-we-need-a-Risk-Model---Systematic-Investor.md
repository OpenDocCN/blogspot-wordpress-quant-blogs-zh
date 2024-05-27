<!--yml

分类：未分类

日期：2024-05-18 14:42:31

-->

# 投资组合优化——为什么我们需要一个风险模型 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/02/26/portfolio-optimization-why-do-we-need-a-risk-model/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/02/26/portfolio-optimization-why-do-we-need-a-risk-model/#0001-01-01)

在前一篇帖子“多元因子模型——构建风险模型”中，我展示了如何构建一个多元因子风险模型。在这篇帖子中，我想解释为什么我们需要一个风险模型以及它在投资组合构建过程中的使用。

协方差矩阵在[均值-方差投资组合优化](http://en.wikipedia.org/wiki/Modern_portfolio_theory)过程中用于估计投资组合风险。样本协方差矩阵可以通过历史资产回报来估计，但是当资产数量（N）与观察数量（T）的量级相同时或更大时，使用样本协方差矩阵就会变得有问题。在典型应用中，可以选择的股票可能超过一千只，但很少有超过十年的月度数据（即 N = 1,000 和 T = 120）。我建议参考以下资料以进行详细讨论：

估计协方差矩阵的一种可能方法是使用低维多元因子模型来建模风险。使用多元因子模型来描述资产之间的协方差的好处之一是，因为协方差矩阵相当稀疏且结构良好，所以投资组合优化算法可以更快地工作。有关详细讨论，请阅读：[投资组合优化与因子、场景和现实短期头寸——B. Jacobs, K. Levy, 和 H. Markowitz (2005)](http://www.jlem.com/articles/jlem/portfolioOptimization.pdf) [在大量证券的问题中，使用密集协方差矩阵（样本协方差矩阵）和使用由多元因子模型允许的对角或接近对角的协方差矩阵，计算时间可能相差一个数量级。]

本文大纲：

+   使用样本协方差矩阵构建最小方差投资组合

+   使用我们前一篇帖子中创建的多元因子风险模型构建最小方差投资组合

让我们首先加载我们在[前一篇帖子](https://systematicinvestor.wordpress.com/2012/02/21/multiple-factor-model-building-risk-model/)末保存的多元因子风险模型。[如果你丢失了 risk.model.Rdata 文件，请首先执行 fm.risk.model.test()函数来创建并保存多元因子风险模型。] 接下来，我将使用历史协方差矩阵构建最小方差投资组合。

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

	# Load factor data that we saved at the end of the fm.all.factor.test function
	load(file='data.factors.Rdata')
		nperiods = nrow(next.month.ret)
		n = ncol(next.month.ret)
		tickers = colnames(next.month.ret)

	# Load multiple factor risk model data that we saved at the end of the fm.risk.model.test function	
	load(file='risk.model.Rdata')

	#*****************************************************************
	# Construct minimum variance portfolio using the sample covariance matrix
	#****************************************************************** 
	load.packages('quadprog,corpcor')

	#--------------------------------------------------------------------------
	# Create Covariance matrix based on the last 24 months of returns
	#--------------------------------------------------------------------------
	temp = last(mlag(next.month.ret),24)
	cov.temp = cov(temp, use='complete.obs', method='pearson')	
	hist.cov = cov.temp

	#--------------------------------------------------------------------------
	# Adjust Covariance matrix
	#--------------------------------------------------------------------------
	if(!is.positive.definite(cov.temp)) {
		cov.temp <- make.positive.definite(cov.temp, 0.000000001)
	}	

	#--------------------------------------------------------------------------
	# Create constraints
	#--------------------------------------------------------------------------
	# set min/max wgts for individual stocks: 0 =< x <= 1
	constraints = new.constraints(n, lb = 0, ub = 1)

	# wgts must sum to 1 (fully invested)
	constraints = add.constraints(rep(1,n), 1, type = '=', constraints)

	#--------------------------------------------------------------------------
	# Solve QP problem
	#--------------------------------------------------------------------------		
	sol = solve.QP.bounds(Dmat = cov.temp, dvec = rep(0, nrow(cov.temp)) , 
		Amat=constraints$A, bvec=constraints$b, constraints$meq,
		lb = constraints$lb, ub = constraints$ub)

	#--------------------------------------------------------------------------
	# Plot Portfolio weights
	#--------------------------------------------------------------------------		
	x = round(sol$solution,4)
		x = iif(x < 0, 0, x)
		names(x) = colnames(next.month.ret)
	hist.min.var.portfolio = x

	# plot
	barplot(100*x,las = 2, 
		main = 'Minimum variance portfolio weights (sample covariance matrix)')		

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/02/plot1-small3.png)

为了最小化在风险模型框架下计算的投资组合风险，我们必须将特定风险和因子协方差矩阵合并为一个协方差矩阵。这个过程在[B. Jacobs, K. Levy, 和 H. Markowitz (2005)所著的《Portfolio Optimization with Factors, Scenarios, and Realistic Short Positions》的第 4-5 页](http://www.jlem.com/articles/jlem/portfolioOptimization.pdf)有描述。

设 K 为风险模型中的因子数量。我们引入 K 个额外的变量，表示投资组合对每个因子的因子暴露。让我们增加 K 个约束条件：

```
X1...Xn * factor.exposures = Xn+1...Xn+k
```

新的协方差矩阵：

```
[specific.risk  0                 ]
[0              factor.covariance ]
```

接下来，我将使用我们在前面的帖子中创建的多因子风险模型构建最小方差投资组合。

```

	#*****************************************************************
	# Construct minimum variance portfolio using the multiple factor risk model
	#****************************************************************** 
	t = nperiods	
	factor.exposures = all.data[t,,-1]	
		nfactors = ncol(factor.exposures)

	#--------------------------------------------------------------------------
	# Create constraints
	#--------------------------------------------------------------------------
	# set min/max wgts for individual stocks: 0 =< x <= 1
	constraints = new.constraints(n, lb = 0, ub = 1)

	# wgts must sum to 1 (fully invested)
	constraints = add.constraints(rep(1,n), 1, type = '=', constraints)

	# adjust prior constraints, add v.i
	constraints = add.variables(nfactors, constraints)

	# BX - Xnew = 0
	constraints = add.constraints(rbind(factor.exposures, -diag(nfactors)), rep(0, nfactors), type = '=', constraints)

	#--------------------------------------------------------------------------
	# Create Covariance matrix
	# [Qu  0]
	# [ 0 Qf]
	#--------------------------------------------------------------------------
	temp = diag(n)
		diag(temp) = specific.variance[t,]²
	cov.temp = diag(n + nfactors)
		cov.temp[1:n,1:n] = temp
	cov.temp[(n+1):(n+nfactors),(n+1):(n+nfactors)] = factor.covariance[t,,]

	#--------------------------------------------------------------------------
	# Solve QP problem
	#--------------------------------------------------------------------------
	load.packages('quadprog')

	sol = solve.QP.bounds(Dmat = cov.temp, dvec = rep(0, nrow(cov.temp)) , 
		Amat=constraints$A, bvec=constraints$b, constraints$meq,
		lb = constraints$lb, ub = constraints$ub)

	#--------------------------------------------------------------------------
	# Plot Portfolio weights
	#--------------------------------------------------------------------------		
	x = round(sol$solution,4)[1:n]
		x = iif(x < 0, 0, x)
		names(x) = colnames(next.month.ret)
	risk.model.min.var.portfolio = x

	# plot
	barplot(100*x,las = 2, 
		main = 'Minimum variance portfolio weights (multiple factor risk model)')

```

![plot2.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/02/plot2-small4.png)

在风险模型下计算的最小方差投资组合更加分散。另外，对于更大的股票池（即 1000-2000 只股票），使用导致稀疏协方差矩阵的因子风险模型解决二次问题将节省时间。

要查看这个例子的完整源代码，请查看[github 上 factor.model.test.r 文件中的 fm.risk.model.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/factor.model.test.r)。
