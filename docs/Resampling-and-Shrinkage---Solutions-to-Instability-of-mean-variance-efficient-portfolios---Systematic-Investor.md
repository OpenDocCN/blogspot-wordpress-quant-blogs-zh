<!--yml

类别：未分类

日期：2024-05-18 14:47:11

-->

# 重采样和收缩：解决均值-方差有效组合的不稳定性 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2011/11/11/resampling-and-shrinkage-solutions-to-instability-of-mean-variance-efficient-portfolios/#0001-01-01`](https://systematicinvestor.wordpress.com/2011/11/11/resampling-and-shrinkage-solutions-to-instability-of-mean-variance-efficient-portfolios/#0001-01-01)

输入假设的小幅变化通常会导致使用均值-方差优化构建的有效组合有很大不同。我将讨论重采样和协方差收缩估计器——两种常见的技术，使均值-方差有效前沿的组合更加多样化，并对输入假设的小幅变化具有免疫力。

重采样是由 Michaud 在《有效的资产管理系统》（第二版）中引入的。[Efficient Asset Management, 2nd edition](http://www.oup.com/us/catalog/general/subject/Finance/Investments/?view=usa&ci=9780195331912)请注意，重采样程序是一个专利组合优化过程。（Richard Michaud 和 Robert Michaud 共同发明人，1999 年 12 月，[美国专利 # 6,003,018](http://www.patentstorm.us/patents/6003018.html)，全球专利申请中）使用包括个人使用在内的这项技术，需要许可或授权。

创建重采样有效前沿：

+   步骤 0：估计均值（Mu*）和协方差（Cov*），例如从历史资产回报中估计。

+   步骤 1：从均值=Mu*和协方差=Cov*的多变量正态分布中抽样。

+   步骤 2：计算样本均值和协方差，并利用它们创建有效前沿。

+   步骤 3：保存位于有效前沿的组合权重。

+   重复步骤 1、2、3 绘制次数的样本。

+   步骤 4：计算保存的组合权重的平均值，以获得位于重采样有效前沿的最终组合权重。

更新：请注意，由于上述专利，我无法发布重采样功能的源代码，这使得下面的示例无法复现。

让我们比较位于均值-方差有效前沿和重采样有效前沿的组合：

```

# load Systematic Investor Toolbox
setInternet2(TRUE)
source(gzcon(url('https://github.com/systematicinvestor/SIT/raw/master/sit.gz', 'rb')))

	#--------------------------------------------------------------------------
	# Create Resampled Efficient Frontier
	#--------------------------------------------------------------------------
	ia = aa.test.create.ia.rebal()
	n = ia$n

	# -1 	constraints = new.constraints(n, lb = 0, ub = 1)

	# SUM x.i = 1
	constraints = add.constraints(rep(1, n), 1, type = '=', constraints)

	# create efficient frontier(s)
	ef.risk = portopt(ia, constraints, 50, 'Risk', equally.spaced.risk = T)
	ef.risk.resampled = portopt.resampled(ia, constraints, 50, 'Risk Resampled',
						nsamples = 200, sample.len= 10)

	# Plot multiple Efficient Frontiers and Transition Maps
	layout( matrix(c(1,1,2,3), nrow = 2, byrow=T) )
	plot.ef(ia, list(ef.risk, ef.risk.resampled), portfolio.risk, F)
	plot.transition.map(ef.risk)
	plot.transition.map(ef.risk.resampled)

```

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot1-small3.png)

重采样有效前沿在视觉上优于均值-方差有效前沿。它更加多样化：所有资产类别的分配存在，组合之间的过渡连续平滑，没有剧烈变化。重采样有效前沿还具有构造上的免疫力，对输入假设的小幅变化免疫。

协方差收缩估计器的想法在 Olivier Ledoit 和 Michael Wolf（2003 年）的《Honey, I Shrunk the Sample Covariance matrix》中很好地解释了。[Honey, I Shrunk the Sample Covariance matrix by Olivier Ledoit and Michael Wolf (2003)](http://www.ledoit.net/honey.pdf)以下是摘要：

[本文的中心论点是，没有人应该用样本协方差矩阵来进行投资组合优化。它包含了最可能扰动均值-方差优化器的估计误差。为此，我们建议使用通过称为收缩的变换从样本协方差矩阵得到的矩阵。这通常会将最极端的系数拉向更集中的值，从而系统地减少在最重要的地方估计误差。从统计学的角度来看，挑战在于知道最优的收缩强度，我们给出了那个公式的。在不改变投资组合优化过程中的其他任何步骤的情况下，我们在实际股票市场数据上显示，收缩相对于基准指数减少了跟踪误差，并且大大增加了积极投资组合经理的实际信息比率。](http://www.ledoit.net/honey_abstract.htm)

Ledoit-Wolf 协方差矩阵估计器是一个凸线性组合 aF + (1-a)S，其中

+   S 是一个样本协方差矩阵。

+   F 是一个高度结构化的估计器。

+   a 是一个收缩常数，介于 0 和 1 之间的一个数字。

这种技术被称为收缩，因为样本协方差矩阵被`收缩’到结构化估计器。收缩目标 F，由常数相关模型建模。该模型认为所有的（成对）相关性都是相同的。所有样本相关性的平均值是共同常数相关性的估计器。

Ledoit-Wolf 协方差收缩估计器在 tawny R 包中实现，cov.shrink 函数。以下是使用 Ledoit-Wolf 协方差收缩估计器的有效前沿示例：

```

#--------------------------------------------------------------------------
# Create Efficient Frontier using Ledoit-Wolf Covariance Shrinkage Estimator from tawny package
#--------------------------------------------------------------------------

# load / check required packages
load.packages('tawny')

ia.original = ia

# compute Ledoit-Wolf Covariance Shrinkage Estimator	
ia$cov = tawny::cov.shrink(ia$hist.returns)	
ef.risk.cov.shrink = portopt(ia, constraints, 50, 'Risk Ledoit-Wolf', equally.spaced.risk = T)

ia = ia.original

# Plot multiple Efficient Frontiers and Transition Maps
layout( matrix(c(1,1,2,3), nrow = 2, byrow=T) )
plot.ef(ia, list(ef.risk, ef.risk.cov.shrink), portfolio.risk, F)	
plot.transition.map(ef.risk)
plot.transition.map(ef.risk.cov.shrink)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot2-small3.png)

使用 Ledoit-Wolf 协方差收缩估计器构建的有效前沿更好：对所有资产类别的分配都存在，并且由于构建方式，对输入假设的小变化具有免疫力。

收缩不是唯一的解决方案，还有许多其他方法可以估计协方差矩阵。例如，Portfolio Probe 博客的 Pat Burns 讨论了使用因子模型估计协方差矩阵：[Ledoit-Wolf 与因子模型的比较](http://www.portfolioprobe.com/2011/04/28/a-test-of-ledoit-wolf-versus-a-factor-model/)。

另一个有趣的想法是将重采样与收缩结合在一起，这在 M. Wolf (2006) 的论文[重采样 vs. 收缩对于基准管理人员](http://www.iew.uzh.ch/wp/iewwp263.pdf)中得到了研究。这个想法很容易实现，因为我们只需要改变上面算法中的第二步。不是使用样本协方差矩阵，我们将使用它的收缩估计器。

让我们比较重采样和重采样+收缩有效前沿：

```

#--------------------------------------------------------------------------
# Create Resampled Efficient Frontier(using Ledoit-Wolf Covariance Shrinkage Estimator)
# As described on page 8 of
# Resampling vs. Shrinkage for Benchmarked Managers by M. Wolf (2006)
#--------------------------------------------------------------------------

ef.risk.resampled.shrink = portopt.resampled(ia, constraints, 50, 'Risk Ledoit-Wolf+Resampled', 
						nsamples = 200, sample.len= 10, 
						shrinkage.fn=tawny::cov.shrink)	

# Plot multiple Efficient Frontiers and Transition Maps
layout( matrix(c(1:4), nrow = 2, byrow=T) )
plot.ef(ia, list(ef.risk, ef.risk.resampled, ef.risk.resampled.shrink), portfolio.risk, F)	
plot.transition.map(ef.risk)
plot.transition.map(ef.risk.resampled)
plot.transition.map(ef.risk.resampled.shrink)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot3-small2.png)

两个前沿非常接近，且投资组合构成非常相似。所以很难说在再抽样算法中增加协方差收缩估计器是否有益。

总之，有研究支持这些方法将提高样本外的回报，也有研究反对。然而，这些方法肯定可以通过使有效前沿的投资组合免疫于输入假设的小变化，从而减少投资组合的换手率和与再平衡相关的交易成本。

在[伍斯特理工学院](http://www.wpi.edu)有一个关于投资组合优化的有趣论文集：

在下一篇文章中，我将讨论 Black-Litterman 模型，该模型解决了均值-方差有效前沿投资组合的不稳定性和多样化问题。

要查看此示例的完整源代码，请查看 github 上的[aa.solutions2instability.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/aa.test.r)。
