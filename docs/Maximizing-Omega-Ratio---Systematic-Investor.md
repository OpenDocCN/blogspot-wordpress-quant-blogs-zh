<!--yml

category: 未分类

date: 2024-05-18 14:47:34

-->

# 最大化 Omega Ratio | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2011/11/03/maximizing-omega-ratio/#0001-01-01`](https://systematicinvestor.wordpress.com/2011/11/03/maximizing-omega-ratio/#0001-01-01)

[Omega Ratio](http://en.wikipedia.org/wiki/Omega_ratio) 是由 [Keating 和 Shadwick](http://faculty.fuqua.duke.edu/~charvey/Teaching/BA453_2006/Keating_An_introduction_to.pdf) 于 2002 年引入的。它衡量了给定目标收益 L 的平均投资组合收益与平均投资组合损失的比率。

设 x.i, i= 1,…,n 为投资组合中各种工具的权重。我们假设有 j= 1,…,T 个具有相等概率的回报场景可用。我将使用历史资产回报作为场景。让我们用 r.ij 表示场景 j 中第 i 个资产的回报。投资组合的 Omega Ratio 可以写成

![\Omega(L) = \frac{E\left [ max(\sum_{i=1}^{n}r_{ij}x_{i} - L, 0) \right ]}{E\left [ max(L - \sum_{i=1}^{n}r_{ij}x_{i}, 0) \right ]}  ](img/7c6ae5b6ac440223dd7e9afdcfed4f65.png)

我将使用 [H. Mausser, D. Saunders, L. Seco (2006)](http://www.math.uwaterloo.ca/~dsaunder/Site/Publications_files/OmegaOptimizationWAppendix.pdf) 论文中提出的方法构建最大化 Omega Ratio 的最优投资组合。

最大化问题（第 5-6 页）可以写成

![\Omega^{*}(L) = max_{x,u,d}\frac{\frac{1}{T} \sum_{i=1}^{n}u_{i}}{\frac{1}{T} \sum_{i=1}^{n}d_{i}}  \newline\newline  \sum_{i=1}^{n}r_{ij}x_{i} - u_{j}+d_{j} = L, j=1,...,T  \newline\newline  u_{j},d_{j}\geq 0, j=1,...,T  \newline\newline  u_{j}*d_{j} = 0, j=1,...,T  ](img/fa37a5489fd92a15e4024551a4d76c66.png)

它可以被表述为一个线性规划问题，其转换如下

![t=\frac{1}{\frac{1}{T} \sum_{i=1}^{n}u_{i}}  \newline\newline  \Omega^{*}(L) = max_{\tilde{x},\tilde{u},\tilde{d},t}\frac{1}{T} \sum_{i=1}^{n}\tilde{u}_{i}  \newline\newline  \sum_{i=1}^{n}r_{ij}\tilde{x}_{i} - \tilde{u}_{j}+\tilde{d}_{j} = L, j=1,...,T  \newline\newline  \frac{1}{T}\sum_{i=1}^{n}\tilde{d}_{i} = 1  \newline\newline  \tilde{u}_{j},\tilde{d}_{j}\geq 0, j=1,...,T  ](img/1f8201cae5584c778215086bf0be1150.png)

这种方法只适用于 ![\Omega^{*}(L) > 1](img/123140917b72af9ad0975a2603a5e3b6.png) 的情况。在 ![\Omega^{*}(L) \leqslant 1](img/778e8ea6f4bbb03715666db080441524.png) 的情况下，我将使用一个非线性规划求解器，[Rdonlp2](http://arumat.net/Rdonlp2/tutorial.html)，它基于由 [彼得·斯佩鲁奇教授](http://www.mathematik.tu-darmstadt.de/fbereiche/numerik/staff/spellucci/spellucci.html) 开发和拥有版权的 donlp2 程序包。由于 Rdonlp2 仅适用于 R 版本 2.9 或更低版本，以下代码在您的计算机上可能无法正确执行。

```

max.omega.portfolio <- function
(
	ia,		# input assumptions
	constraints	# constraints
)
{
	n = ia$n
	nt = nrow(ia$hist.returns)

	constraints0 = constraints

	omega = ia$parameters.omega	

	#--------------------------------------------------------------------------
	# Linear Programming, Omega > 1, Case
	#--------------------------------------------------------------------------

	# objective : Omega
	# [ SUM <over j> 1/T * u.j ]
	f.obj = c(rep(0, n), (1/nt) * rep(1, nt), rep(0, nt), 0)

	# adjust constraints, add u.j, d.j, t
	constraints = add.variables(2*nt + 1, constraints, lb = c(rep(0,2*nt),-Inf))

	# Transformation for inequalities
	# Aw < b => Aw1 - bt < 0
	constraints$A[n + 2*nt + 1, ] = -constraints$b
	constraints$b[] = 0	

	# Transformation for Lower/Upper bounds, use same transformation
	index = which( constraints$ub[1:n] < +Inf )	
	if( len(index) > 0 ) {			
		a = rbind( diag(n), matrix(0, 2*nt, n), -constraints$ub[1:n])		
		constraints = add.constraints(a[, index], rep(0, len(index)), '<=', constraints)			
	}

	index = which( constraints$lb[1:n] > -Inf )	
	if( len(index) > 0 ) {	
		a = rbind( diag(n), matrix(0, 2*nt, n), -constraints$lb[1:n])		
		constraints = add.constraints(a[, index], rep(0, len(index)), '>=', constraints)					
	}

	constraints$lb[1:n] = -Inf
	constraints$ub[1:n] = Inf

	# [ SUM <over i> r.ij * x.i ] - u.j + d.j - L * t = 0, for each j = 1,...,T 	
	a = rbind( matrix(0, n, nt), -diag(nt), diag(nt), -omega)
		a[1 : n, ] = t(ia$hist.returns)
	constraints = add.constraints(a, rep(0, nt), '=', constraints)			

	# [ SUM <over j> 1/T * d.j ] = 1	
	constraints = add.constraints(c( rep(0,n), rep(0,nt), (1/nt) * rep(1,nt), 0), 1, '=', constraints)				

	# setup linear programming
	f.con = constraints$A
	f.dir = c(rep('=', constraints$meq), rep('>=', len(constraints$b) - constraints$meq))
	f.rhs = constraints$b

	# find optimal solution
	x = NA
	sol = try(solve.LP.bounds('max', f.obj, t(f.con), f.dir, f.rhs,
					lb = constraints$lb, ub = constraints$ub), TRUE)

	if(!inherits(sol, 'try-error')) {
		x0 = sol$solution[1:n]
		u = sol$solution[(1+n):(n+nt)]
		d = sol$solution[(n+nt+1):(n+2*nt)] 
		t = sol$solution[(n+2*nt+1):(n+2*nt+1)] 

		# Reverse Transformation	
		x = x0/t
	}

	#--------------------------------------------------------------------------
	# NonLinear Programming, Omega > 1, Case
	#--------------------------------------------------------------------------
	# Check if any u.j * d.j != 0 or LP solver encounter an error
	if( any( u*d != 0 ) || sol$status !=0 ) {
		require(Rdonlp2)

		constraints = constraints0

		# compute omega ratio
		fn <- function(x){
			portfolio.returns = x %*% t(ia$hist.returns)	
			mean(pmax(portfolio.returns - omega,0)) / mean(pmax(omega - portfolio.returns,0))
		}

		# control structure, fnscale - set -1 for maximization
		cntl <- donlp2.control(silent = T, fnscale = -1, iterma =10000, nstep = 100, epsx = 1e-10)	

		# lower/upper bounds
		par.l = constraints$lb
		par.u = constraints$ub

		# intial guess
		if(!is.null(constraints$x0)) p = constraints$x0

		# linear constraints
		A = t(constraints$A)
		lin.l = constraints$b
		lin.u = constraints$b
		lin.u[ -c(1:constraints$meq) ] = +Inf

		# find solution
		sol = donlp2(p, fn, par.lower=par.l, par.upper=par.u, 
			A=A, lin.u=lin.u, lin.l=lin.l, control=cntl)
		x = sol$par
	}

	return( x )
}

```

首先让我们看一下传统的均值-方差有效前沿在 Omega Ratio 框架中的样子。

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

	# Omega - http://en.wikipedia.org/wiki/Omega_ratio
	ia$parameters.omega = 13/100 
		ia$parameters.omega = 12/100 
		# convert annual to monthly
		ia$parameters.omega = ia$parameters.omega / 12

	# create efficient frontier(s)
	ef.risk = portopt(ia, constraints, 50, 'Risk')

	# Plot Omega Efficient Frontiers and Transition Maps
	layout( matrix(1:4, nrow = 2, byrow=T) )

	# weights
	rownames(ef.risk$weight) = paste('Risk','weight',1:50,sep='_')
	plot.omega(ef.risk$weight[c(1,10,40,50), ], ia)

	# assets
	temp = diag(n)
	rownames(temp) = ia$symbols
	plot.omega(temp, ia)

	# mean-variance efficient frontier in the Omega Ratio framework
	plot.ef(ia, list(ef.risk), portfolio.omega, T, T)			

```

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot1-small1.png)

在 Omega Ratio 框架下，随着我们沿着传统的均值-方差有效前沿移动，投资组合的回报和投资组合 Omega 比率单调递增。风险最小的组合（Risk_weight_1, Risk_weight_10）对于 13%的阈值（目标回报）具有较低的 Omega 比率，而风险最大的组合（Risk_weight_40, Risk_weight_50）具有较高的 Omega 比率。

为了在 Omega Ratio 框架下创建有效前沿，我建议首先计算均值-方差框架中的回报范围。接下来，将这个范围分成#个等距的组合点。对于每个点，我建议找到一个组合，其预期回报小于给定点的预期回报且具有最大 Omega 比率。

```

#--------------------------------------------------------------------------
# Create Efficient Frontier in Omega Ratio framework
#--------------------------------------------------------------------------
	# Create maximum Omega Efficient Frontier
	ef.omega = portopt.omega(ia, constraints, 50, 'Omega')

	# Plot Omega Efficient Frontiers and Transition Maps
	layout( matrix(1:4, nrow = 2, byrow=T) )

	# weights
	plot.omega(ef.risk$weight[c(1,10,40,50), ], ia)

	# weights
	rownames(ef.omega$weight) = paste('Omega','weight',1:50,sep='_')	
	plot.omega(ef.omega$weight[c(1,10,40,50), ], ia)

	# portfolio
	plot.ef(ia, list(ef.omega, ef.risk), portfolio.omega, T, T)			

```

![plot2.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot2-small1.png)

Omega Ratio 有效前沿与预期回报大于 13%阈值（目标回报）的传统均值-方差有效前沿相似。然而，对于预期回报小于 13%阈值的组合，分配发生了巨大转变，并且 Omega 比率有所增加。

![plot3.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot3-small.png)

在风险框架下，对于预期回报小于 13%阈值的组合，Omega Ratio 有效前沿显得非常低效。但请记住，此优化的目标是找到最大化 Omega Ratio 的组合，给定用户的约束。总的来说，我发现对于预期回报小于 13%阈值的组合的结果有些激进，这些结果绝对需要进一步调查。

要查看此示例的完整源代码，请查看 github 上的[aa.omega.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/aa.test.r)。
