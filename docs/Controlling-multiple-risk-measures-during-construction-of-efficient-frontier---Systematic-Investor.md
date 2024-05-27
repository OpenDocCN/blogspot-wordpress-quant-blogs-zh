让我们使用[资产配置简介](https://systematicinvestor.wordpress.com/2011/10/13/introduction-to-asset-allocation/)帖子中提供的历史输入假设来检查使用不同风险度量计算的有效前沿：

日期: 2024-05-18 14:47:54

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/10/plot1-small7.png)

在过去的几篇文章中，我介绍了[最大损失，均值绝对偏差](https://systematicinvestor.wordpress.com/2011/10/14/maximum-loss-and-mean-absolute-deviation-risk-measures/)，以及[预期损失（CVaR）和条件回撤风险（CDaR）](https://systematicinvestor.wordpress.com/2011/10/25/expected-shortfall-cvar-and-conditional-drawdown-at-risk-cdar-risk-measures/)风险度量。 这些风险度量可以被制定为线性约束，因此可以在有效前沿的构建过程中结合起来控制多种风险度量。

# <!--yml

> 要查看此示例和其他示例的完整源代码，请查看 [github 上 aa.test.r 中的 aa.multiple.risk.measures.test() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/aa.test.r)。

来源：[`systematicinvestor.wordpress.com/2011/10/26/controlling-multiple-risk-measures-during-construction-of-efficient-frontier/#0001-01-01`](https://systematicinvestor.wordpress.com/2011/10/26/controlling-multiple-risk-measures-during-construction-of-efficient-frontier/#0001-01-01)

为了构建一个新的均值方差有效前沿，其中只包含最大损失小于 12% 的投资组合

```

# load Systematic Investor Toolbox
setInternet2(TRUE)
source(gzcon(url('https://github.com/systematicinvestor/SIT/raw/master/sit.gz', 'rb')))

#--------------------------------------------------------------------------
# Create Efficient Frontier
#--------------------------------------------------------------------------
	ia = aa.test.create.ia()
	n = ia$n		

	# 0 <= x.i <= 0.8
	constraints = new.constraints(n, lb = 0, ub = 0.8)

	# SUM x.i = 1
	constraints = add.constraints(rep(1, n), 1, type = '=', constraints)		

	# create efficient frontier(s)
	ef.risk = 	portopt(ia, constraints, 50, 'Risk')
	ef.maxloss = 	portopt(ia, constraints, 50, 'MaxLoss',	min.maxloss.portfolio)

	# Plot multiple Efficient Frontiers
	layout( matrix(1:4, nrow = 2) )
	plot.ef(ia, list(ef.risk, ef.maxloss), portfolio.risk, F)	
	plot.ef(ia, list(ef.risk, ef.maxloss), portfolio.maxloss, F)	

	plot.transition.map(ef.risk)
	plot.transition.map(ef.maxloss)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/10/plot2-small7.png)

类别: 未分类

```

	#--------------------------------------------------------------------------
	# Add MaxLoss <= 12 constraint
	#--------------------------------------------------------------------------

	constraints = add.constraint.maxloss(ia, 12/100, '<=', constraints)	

	ef.risk.maxloss = portopt(ia, constraints, 50, 'Risk+MaxLoss')
		ef.risk.maxloss$weight = ef.risk.maxloss$weight[, 1:n]

	# Plot multiple Efficient Frontiers
	layout( matrix(1:4, nrow = 2) )
	plot.ef(ia, list(ef.risk.maxloss, ef.risk, ef.maxloss), portfolio.risk, F)	
	plot.ef(ia, list(ef.risk.maxloss, ef.risk, ef.maxloss), portfolio.maxloss, F)	

	plot.transition.map(ef.risk)
	plot.transition.map(ef.risk.maxloss)

```

新的有效前沿，标记为‘风险+最大损失’，位于风险和最大损失有效前沿之间，无论是按标准偏差衡量的风险，还是按最大损失衡量的风险图中都是如此。 原始‘风险’和新‘风险+最大损失’投资组合之间的主要区别可以从它们的过渡图中看出。 为了在均值方差优化期间控制最大损失，‘风险+最大损失’投资组合不分配给新兴市场（EEM - 用绿色突出显示）。

-->

在构建有效前沿期间控制多种风险度量 | Systematic Investor
