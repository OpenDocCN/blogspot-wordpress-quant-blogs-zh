<!--yml

类别：未分类

日期：2024-05-18 14:37:26

-->

# 最小相关算法速度比较 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2012/09/26/minimum-correlation-algorithm-speed-comparison/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/09/26/minimum-correlation-algorithm-speed-comparison/#0001-01-01)

[最小相关算法](https://systematicinvestor.wordpress.com/2012/09/22/minimum-correlation-algorithm-paper/)是由[大卫·瓦拉迪](http://cssanalytics.wordpress.com/2012/09/21/minimum-correlation-algorithm-paper-release/)发现的一种启发式方法。下面我将比较最小相关算法的两个版本与传统的最小方差优化方法的执行速度，后者依赖于解决一个二次规划问题。

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)
# https://systematicinvestor.wordpress.com/systematic-investor-toolbox/
###############################################################################
setInternet2(TRUE)
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

	#*****************************************************************
	# Setup test input assumptions
	#*****************************************************************
	load.packages('quadprog,corpcor')

	n = 100
	hist = matrix(rnorm(1000*n), nc=n)

	# 0 <= x.i <= 1
	constraints = new.constraints(n, lb = 0, ub = 1)
		constraints = add.constraints(diag(n), type='>=', b=0, constraints)
		constraints = add.constraints(diag(n), type='<=', b=1, constraints)

	# SUM x.i = 1
	constraints = add.constraints(rep(1, n), 1, type = '=', constraints)		

	# create historical input assumptions
	ia = list()
		ia$n = n
		ia$risk = apply(hist, 2, sd)
		ia$correlation = cor(hist, use='complete.obs', method='pearson')
		ia$cov = ia$correlation * (ia$risk %*% t(ia$risk))

		ia$cov = make.positive.definite(ia$cov, 0.000000001)
		ia$correlation = make.positive.definite(ia$correlation, 0.000000001)

	#*****************************************************************
	# Time each Algorithm 
	#*****************************************************************				
	load.packages('rbenchmark')			

	benchmark(
		min.var.portfolio(ia, constraints),
		min.corr.portfolio(ia, constraints),
		min.corr2.portfolio(ia, constraints),

	columns=c("test", "replications", "elapsed", "relative"),
	order="relative",
	replications=100
	)

```

我运行了上述代码，n=10（10 个资产），n=100（100 个资产），n=500（500 个资产），n=1000（1000 个资产）。

[请注意，对于 n=1000 我只运行了 5 次复制]

```

n=10 (10 assets)
                      replications elapsed relative
   min.var.portfolio          100    0.02      1.0
 min.corr2.portfolio          100    0.02      1.0
  min.corr.portfolio          100    0.03      1.5

n=100 (100 assets)
                      replications elapsed relative
 min.corr2.portfolio          100    0.07 1.00
  min.corr.portfolio          100    0.25 3.57
   min.var.portfolio          100    0.31 4.42

n=500 (500 assets)
                      replications elapsed  relative
 min.corr2.portfolio          100    2.18  1.00
  min.corr.portfolio          100    9.59  4.39
   min.var.portfolio          100  139.13 63.82

n=1000 (1000 assets) 
                      replications elapsed relative
 min.corr2.portfolio            5    0.25     1.00
  min.corr.portfolio            5    1.39     5.56
   min.var.portfolio            5  113.27   453.08

```

对于小宇宙（即 n ~ 100）所有算法都很快。但是一旦我们尝试解决 500 个或 1000 个资产的投资组合分配问题，最小方差算法比最小相关算法的两个版本慢得多。

所以，如果我们考虑对 10 年内的 500 个资产进行每周回测，运行时间（即秒，52*10*单次调整时间）：

```

                            elapsed
 min.corr2.portfolio          11.3
  min.corr.portfolio          49.8
   min.var.portfolio         723.4

```

要查看此示例的完整源代码，请查看 github 上的 [bt.mca.speed.test() 函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
