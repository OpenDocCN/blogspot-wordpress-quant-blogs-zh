<!--yml

类别：未分类

日期：2024-05-18 14:48:38

-->

# 最多元化或最不相关的有效前沿 | 系统性投资者

> 来源：[`systematicinvestor.wordpress.com/2011/10/27/the-most-diversified-or-the-least-correlated-efficient-frontier/#0001-01-01`](https://systematicinvestor.wordpress.com

[“最小相关算法”](http://cssanalytics.wordpress.com/2011/08/09/forecast-free-algorithms-a-new-benchmark-for-tactical-strategies/) 是我在 [CSS Analytics 博客](http://cssanalytics.wordpress.com) 上偶然发现的一个术语。这是一个有趣的风险度量，在我的解释中意味着：在给定收益水平下最小化每个资产类别与平均投资组合的相关性。

有人可能会尝试在均值-方差优化中使用相关性而不是协方差矩阵，但正如我将在下面展示的那样，这种方法不会产生最不相关的投资组合。

每个资产类别与平均投资组合相关性：

![P = \sum_{i=1}^{n}w_{i}X_{i} = w^{T} \ast X  \newline\newline  \sigma_{P} = w^{T} \ast COV \ast w  \newline\newline  COV\left ( P,X_{i} \right ) = COV\left ( \sum_{i=1}^{n}w_{i}X_{i},X_{i} \right )  =w_{1}COV\left ( X_{1},X_{i} \right )+...+w_{n}COV\left ( X_{n},X_{i} \right )  \newline\newline  \rho_{P,X_{i}} = \frac{COV\left ( P,X_{i} \right )}{\sigma_{P}\ast\sigma_{X_{i}}}  \newline\newline  Average Portfolio Correlation = \frac{1}{n}\sum_{i=1}^{n}\rho_{P,X_{i}}  ](img/852fcb71f1ba0df8b08471828476ec8d.png)

这个公式可以很容易地用 R 代码编写：

```

portfolio.sigma = sqrt( t(weight) %*% assets.cov %*% weight )
mean( ( weight %*% assets.cov ) / ( assets.sigma * portfolio.sigma ) )

# Alternatively
portfolio.returns = weight %*% t(assets.hist.returns)	
mean(cor(assets.hist.returns, portfolio.returns)) 

```

我不知道如何将这个公式转化为线性规划，所以我将使用一个非线性规划求解器，[Rdonlp2](http://arumat.net/Rdonlp2/tutorial.html)，这是基于由[彼得·斯佩鲁奇教授](http://www.mathematik.tu-darmstadt.de/fbereiche/numerik/staff/spellucci/spellucci.html)开发和版权的 donlp2 例程。由于 Rdonlp2 仅适用于 R 版本 2.9 或更低版本，以下代码可能无法在您的计算机上正确执行。

```

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
	ef.risk = portopt(ia, constraints, 50, 'Risk')
	ef.cor.insteadof.cov = portopt(ia, constraints, 50, 'Cor instead of Cov', min.cor.insteadof.cov.portfolio)
	ef.avgcor = portopt(ia, constraints, 50, 'AvgCor', min.avgcor.portfolio)

	# Plot multiple Efficient Frontiers	
	layout(1:2)
	plot.ef(ia, list(ef.risk, ef.avgcor, ef.cor.insteadof.cov), portfolio.risk, F)	
	plot.ef(ia, list(ef.risk, ef.avgcor, ef.cor.insteadof.cov), portfolio.avgcor, F)	

	# Plot multiple Transition Maps	
	layout( matrix(1:4, nrow = 2) )
	plot.transition.map(ef.risk)
	plot.transition.map(ef.avgcor)
	plot.transition.map(ef.cor.insteadof.cov)

	# visualize input assumptions
	plot.ia(ia)

```

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/10/plot1-small8.png)

在均值-方差优化中使用相关性而不是协方差矩阵是一个非常糟糕的想法，因为它会产生最不相关的投资组合。与标准的“风险”有效前沿相比，“Cor instead of Cov”有效前沿实际上会增加平均投资组合的相关性。

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/10/plot2-small8.png)

平均相关性有效前沿的投资组合构成在低风险水平下分为黄金（GLD）和债券（TLT）。这并不令人惊讶，因为黄金和债券都具有正的预期收益率，并且与其他资产的相关性较低。

![plot3.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/10/plot3-small5.png)

要查看此示例的完整源代码，请查看[GitHub 上的 aa.avg.cor.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/aa.test.r)。

以下是用于最小化每种资产类别之间平均投资组合相关性的完整源代码：

```

min.avgcor.portfolio <- function
(
	ia,			# input assumptions
	constraints		# constraints
)
{
	require(Rdonlp2)

	cov = ia$cov[1:ia$n, 1:ia$n]
	s = sqrt(diag(cov))

	# avgcor
	fn <- function(x){
		sd_x = sqrt( t(x) %*% cov %*% x )
		mean( ( x %*% cov ) / ( s * sd_x ) )
	}

	# control structure
	cntl <- donlp2.control(silent = T, iterma =10000, nstep = 100, epsx = 1e-10)	

	# lower/upper bounds
	par.l = constraints$lb
	par.u = constraints$ub

	# intial guess
	p = rep(1,n)
	if(!is.null(constraints$x0)) p = constraints$x0

	# linear constraints
	A = t(constraints$A)
	lin.l = constraints$b
	lin.u = constraints$b
	lin.u[ -c(1:constraints$meq) ] = +Inf

	# find solution
	sol = donlp2(p, fn, 
			par.lower=par.l, par.upper=par.u, 
			A=A, lin.u=lin.u, lin.l=lin.l, 
			control=cntl)
	x = sol$par

	return( x )
}

```
