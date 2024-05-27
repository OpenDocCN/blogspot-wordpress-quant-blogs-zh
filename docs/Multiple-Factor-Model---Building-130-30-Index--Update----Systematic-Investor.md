<!--yml

类别：未分类

日期：2024-05-18 14:42:14

-->

# 多因子模型 – 构建 130/30 指数（更新） | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/03/10/multiple-factor-model-building-13030-index-update/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/03/10/multiple-factor-model-building-13030-index-update/#0001-01-01)

这只是一个对我在上篇文章的快速更新：[多因子模型 - 构建 130/30 指数](https://systematicinvestor.wordpress.com/2012/03/06/multiple-factor-model-building-13030-index/)。我想介绍市场中性策略和最小方差策略，并比较它们与 130/30 指数的表现。

我已经更新了[github 上因子模型测试文件中的 fm.long.short.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/factor.model.test.r)，包括市场中性策略和最小方差策略。

让我们先创建一个最小方差策略。我将使用与[多因子模型 - 构建 130/30 指数](https://systematicinvestor.wordpress.com/2012/03/06/multiple-factor-model-building-13030-index/)文章相同的框架。在每个月底，我将解决一个最小方差的组合，忽略所有的 alpha 信息。

```

	#*****************************************************************
	# Construct LONG ONLY minimum variance portfolio using the multiple factor risk model
	#****************************************************************** 
	weights$long.min.var.alpha = weight

	for(t in 36:nperiods) {	
		#--------------------------------------------------------------------------
		# Create constraints
		#--------------------------------------------------------------------------
		# set min/max wgts for individual stocks: 0 =< x <= 10/100
		constraints = new.constraints(n, lb = 0, ub = 10/100)

		# wgts must sum to 1 (fully invested)
		constraints = add.constraints(rep(1,n), type = '=', b = 1, constraints)

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
		# Setup optimizations
		#--------------------------------------------------------------------------	
		# set expected return
		alpha = factors.avg$AVG[t,] / 5
		expected.return = c(ifna(coredata(alpha),0), rep(0, nfactors))

		# remove companies that have no beta from optimization
		index = which(is.na(beta[t,]))
		if( len(index) > 0) {
			constraints$ub[index] = 0
			constraints$lb[index] = 0
		}

		# find solution
		sol = solve.QP.bounds(Dmat = cov.temp, dvec = 0 * expected.return, 
					Amat = constraints$A, bvec = constraints$b, 
					meq = constraints$meq, lb = constraints$lb, ub = constraints$ub)

		weights$long.min.var.alpha[t,] = sol$solution[1:n]

		cat(t, '\n')
	}

```

接下来，让我们构建市场中性投资组合。我将限制投资组合权重为±10%，并将使用我在[130/30 投资组合建设](https://systematicinvestor.wordpress.com/2011/10/18/13030-porfolio-construction/)文章中记录的投资组合建设技术。

```

	#*****************************************************************
	# Construct Market-Neutral portfolio 100:100 with beta=0 using the multiple factor risk model
	# based on the examples in the aa.long.short.test functions
	#****************************************************************** 
	weights$market.neutral.alpha = weight

	for(t in 36:nperiods) {	
		#--------------------------------------------------------------------------
		# Split x into x.long and x.short, x_long and x_short >= 0
		# SUM(x.long) - SUM(x.short) = 0
		#--------------------------------------------------------------------------			
		# x.long and x.short >= 0
		# x.long <= 0.1 
		# x.short <= 0.1 
		constraints = new.constraints(2*n, lb = 0, ub = c(rep(0.1,n), rep(0.1,n)))

		# SUM (x.long - x.short) = 0
		constraints = add.constraints(c(rep(1,n), -rep(1,n)), 0, type = '=', constraints)		

		# SUM (x.long + x.short) = 2
		constraints = add.constraints(c(rep(1,n), rep(1,n)), 2, type = '=', constraints)		

		#--------------------------------------------------------------------------
		# beta of portfolio is the weighted average of the individual asset betas		
		# http://www.duke.edu/~charvey/Classes/ba350/riskman/riskman.htm
		#--------------------------------------------------------------------------
		temp = ifna(as.vector(beta[t,]),0)
		constraints = add.constraints(c(temp, -temp), type = '=', b = 0, constraints)

		#--------------------------------------------------------------------------
		# Create factor exposures constraints
		#--------------------------------------------------------------------------	
		# adjust prior constraints, add factor exposures
		constraints = add.variables(nfactors, constraints)

		# BX - X1 = 0
		temp = ifna(factor.exposures[t,,], 0)
		constraints = add.constraints(rbind(temp, -temp, -diag(nfactors)), rep(0, nfactors), type = '=', constraints)

		#--------------------------------------------------------------------------
		# Add binary constraints	
		#--------------------------------------------------------------------------	
		# adjust prior constraints: add b.i
		constraints = add.variables(n, constraints)

		# index of binary variables b.i
		constraints$binary.index = (2*n + nfactors + 1):(3*n + nfactors)

		# binary variable b.i : x.long < b, x.short < (1 - b)
		# x.long < b
		constraints = add.constraints(rbind(diag(n), 0*diag(n), matrix(0,nfactors,n), -diag(n)), rep(0, n), type = '<=', constraints)

		# x.short < (1 - b)
		constraints = add.constraints(rbind(0*diag(n), diag(n), matrix(0,nfactors,n), diag(n)), rep(1, n), type = '<=', constraints)

		#--------------------------------------------------------------------------
		# set expected return
		#--------------------------------------------------------------------------	
		# set expected return
		alpha = factors.avg$AVG[t,] / 5
		temp = ifna(coredata(alpha),0)
		expected.return = c(temp, -temp, rep(0, nfactors), rep(0, n))

		#--------------------------------------------------------------------------
		# Create Covariance matrix
		# [Qu  0]
		# [ 0 Qf]
		#--------------------------------------------------------------------------
		temp = diag(n)
			diag(temp) = ifna(specific.variance[t,], mean(coredata(specific.variance[t,]), na.rm=T))²

		# | cov -cov |
		# |-cov  cov |		
		temp = cbind( rbind(temp, -temp), rbind(-temp, temp) )

		cov.temp = 0*diag(2*n + nfactors + n)
			cov.temp[1:(2*n),1:(2*n)] = temp
		cov.temp[(2*n+1):(2*n+nfactors),(2*n+1):(2*n+nfactors)] = factor.covariance[t,,]

		#--------------------------------------------------------------------------
		# Adjust Covariance matrix
		#--------------------------------------------------------------------------
		if(!is.positive.definite(cov.temp)) {
			cov.temp <- make.positive.definite(cov.temp, 0.000000001)
		}	

		#--------------------------------------------------------------------------
		# page 9, Risk: We use the Barra default setting, risk aversion value of 0.0075, and
		# AS-CF risk aversion ratio of 1.
		#
		# The Effects of Risk Aversion on Optimization (2010) by S. Liu, R. Xu
		# page 4/5
		#--------------------------------------------------------------------------
		risk.aversion = 0.0075

		# remove companies that have no beta from optimization
		index = which(is.na(beta[t,]))
		if( len(index) > 0) {
			constraints$ub[index] = 0
			constraints$lb[index] = 0
			constraints$ub[2*index] = 0
			constraints$lb[2*index] = 0			
		}

		# find solution
		sol = solve.QP.bounds(Dmat = 2* risk.aversion * cov.temp, dvec = expected.return, 
					Amat = constraints$A, bvec = constraints$b, 
					meq = constraints$meq, lb = constraints$lb, ub = constraints$ub,
					binary.vec = constraints$binary.index)					

		x = sol$solution[1:n] - sol$solution[(n+1):(2*n)]
		weights$market.neutral.alpha[t,] = x

		cat(t, '\n')
	}

```

接下来，让我们重新创建[多因子模型 - 构建 130/30 指数](https://systematicinvestor.wordpress.com/2012/03/06/multiple-factor-model-building-13030-index/)帖子中的所有摘要图表。

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/03/plot1-small1.png)

![plot2.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/03/plot2-small1.png)

![plot3.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/03/plot3-small1.png)

![plot4.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/03/plot4-small1.png)

请注意，我们这里并不是在比较苹果和苹果。例如，市场中性策略的贝塔值设为零，而 130/30 指数的贝塔值设为 one。但与此同时，也有几个有趣的观察结果：

+   最小方差策略在所有长期策略中跌幅最小，但其表现不足

+   市场中性策略在这种环境中表现出色，具有最佳的夏普比率

+   市场中性策略的组合换手率也最高；因此，高交易成本将使这种策略变得不那么有吸引力

要查看本例的完整源代码，请查看[github 上的 factor.model.test.r 文件中的 fm.long.short.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/factor.model.test.r)。
