<!--yml
category: 未分类
date: 2024-05-18 14:37:26
-->

# Minimum Correlation Algorithm Speed comparison | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2012/09/26/minimum-correlation-algorithm-speed-comparison/#0001-01-01](https://systematicinvestor.wordpress.com/2012/09/26/minimum-correlation-algorithm-speed-comparison/#0001-01-01)

[The Minimum Correlation Algorithm](https://systematicinvestor.wordpress.com/2012/09/22/minimum-correlation-algorithm-paper/) is a heuristic method discovered by [David Varadi](http://cssanalytics.wordpress.com/2012/09/21/minimum-correlation-algorithm-paper-release/). Below I will benchmark the execution speed of 2 versions of the Minimum Correlation Algorithm versus the traditional minimum variance optimization that relies on solving a quadratic programming problem.

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

I have run the code above for n=10 (10 assets), n=100 (100 assets), n=500 (500 assets), n=1000 (1000 assets)
[Please note that for n=1000 I have only run 5 replication]

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

For small universe (i.e. n ~ 100) all algorithms are fast. But once we attempt to solve 500 or 1000 assets portfolio allocation problem, the minimum variance algorithm is many times slower than the both versions of the minimum correlation algorithm.

So if we are considering a 500 assets weekly back-test for the 10 yrs the run-times in seconds (i.e. 52*10*single tun-time):

```

                            elapsed
 min.corr2.portfolio          11.3
  min.corr.portfolio          49.8
   min.var.portfolio         723.4

```

To view the complete source code for this example, please have a look at the [bt.mca.speed.test() function in bt.test.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r).