<!--yml
category: 未分类
date: 2024-05-18 14:47:11
-->

# Resampling and Shrinkage : Solutions to Instability of mean-variance efficient portfolios | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2011/11/11/resampling-and-shrinkage-solutions-to-instability-of-mean-variance-efficient-portfolios/#0001-01-01](https://systematicinvestor.wordpress.com/2011/11/11/resampling-and-shrinkage-solutions-to-instability-of-mean-variance-efficient-portfolios/#0001-01-01)

Small changes in the input assumptions often lead to very different efficient portfolios constructed with mean-variance optimization. I will discuss Resampling and Covariance Shrinkage Estimator – two common techniques to make portfolios in the mean-variance efficient frontier more diversified and immune to small changes in the input assumptions.

Resampling was introduced by Michaud in [Efficient Asset Management, 2nd edition](http://www.oup.com/us/catalog/general/subject/Finance/Investments/?view=usa&ci=9780195331912). Please note that the Resampling procedure is patented portfolio optimization process. (Richard Michaud and Robert Michaud co-inventors, December 1999, [U.S. Patent # 6,003,018](http://www.patentstorm.us/patents/6003018.html), worldwide patents pending) The use of this technology that includes include even personal use, requires licensing or authorization.

To create Resampled Efficient Frontier:

*   Step 0: Estimate mean (Mu*) and covariance (Cov*), for example from historical assets returns.
*   Step 1: Sample from multivariate normal distribution with mean=Mu* and covariance=Cov*.
*   Step 2: Compute sample mean and covariance, and use them to create efficient frontier.
*   Step 3: Save portfolio weights that are on efficient frontier.
*   Repeat Steps 1,2,3 Number of Samples to draw times.
*   Step 4: Average over saved portfolio weights to obtain final portfolio weights that lie on the Resampled Efficient Frontier.

*Update: please note that due to the above patent, I cannot post the source code for the resampling function and that makes examples below not reproducible.*

Let’s compare portfolios that lie on the mean-variance efficient frontier and Resampled efficient frontier:

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

[![](img/c6d396d7be76c90fde0dde67c0cd3f7d.png "plot1.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot1-small3.png)

The Resampled Efficient Frontier is visually superior to the the mean-variance efficient frontier. It is better Diversified: allocation to all asset classes is present and transition between portfolios is continuous and smooth, no sharp changes. The Resampled Efficient Frontier is also, by construction, immune to small changes in the input assumptions.

The idea of Covariance Shrinkage Estimator is nicely explained at [Honey, I Shrunk the Sample Covariance matrix by Olivier Ledoit and Michael Wolf (2003)](http://www.ledoit.net/honey.pdf). Here is the Abstract:

[The central message of this paper is that nobody should be using the sample covariance matrix for the purpose of portfolio optimization. It contains estimation error of the kind most likely to perturb a mean-variance optimizer. In its place, we suggest using the matrix obtained from the sample covariance matrix through a transformation called shrinkage. This tends to pull the most extreme coefficients towards more central values, thereby systematically reducing estimation error where it matters most. Statistically, the challenge is to know the optimal shrinkage intensity, and we give the formula for that. Without changing any other step in the portfolio optimization process, we show on actual stock market data that shrinkage reduces tracking error relative to a benchmark index, and substantially increases the realized information ratio of the active portfolio manager.](http://www.ledoit.net/honey_abstract.htm)

The Ledoit-Wolf Covariance Matrix Estimator is a convex linear combination aF + (1-a)S, where

*   S is a sample covariance matrix,
*   F is a highly structured estimator,
*   a is a shrinkage constant, a number between 0 and 1.

This technique is called shrinkage, since the sample covariance matrix is `shrunk’ to-wards the structured estimator. The Shrinkage Target, F, is modeled by constant correlation model. The model says that all the (pairwise) correlations are identical. The average of all the sample correlations is the estimator of the common constant correlation.

The Ledoit-Wolf Covariance Shrinkage Estimator is implemented in tawny R package, cov.shrink function. Here is an example of efficient frontier using the Ledoit-Wolf Covariance Shrinkage Estimator:

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

[![](img/98457d2cb96c6c203856baaaabaae866.png "plot2.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot2-small3.png)

The Efficient Frontier constructed with Ledoit-Wolf Covariance Shrinkage Estimator is better Diversified: allocation to all asset classes is present and is also, by construction, immune to small changes in the input assumptions.

Shrinkage is not the only solution, there are many alternatives ways to estimate Covariance matrix. For example, Pat Burns at Portfolio Probe blog, discusses estimation of Covariance matrix with factor models: [A test of Ledoit-Wolf versus a factor model](http://www.portfolioprobe.com/2011/04/28/a-test-of-ledoit-wolf-versus-a-factor-model/).

Another interesting idea is to combine Resampling with Shrinkage was examined in the [Resampling vs. Shrinkage for Benchmarked Managers by M. Wolf (2006)](http://www.iew.uzh.ch/wp/iewwp263.pdf) paper. It is very easy to implement because we only need to change Step 2 in the above algorithm. Instead of using sample covariance matrix, we will use it’s Shrinkage Estimator.

Let’s compare Resampled and Resampled+Shrinkage Efficient Frontiers:

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

[![](img/c127944c7ae6d3d74adafeaba2b99033.png "plot3.png.small")](https://systematicinvestor.wordpress.com/wp-content/uploads/2011/11/plot3-small2.png)

Both frontiers are close and have very similar portfolio composition. So it’s hard to say if adding covariance shrinkage estimator to the resampling algorithm is beneficial.

In conclusion, there are findings for and against that these methods will improve out-of-sample returns. However, these methods will surely reduce portfolio turnover and transaction cost associated with rebalancing by making portfolios on efficient frontier immune to small changes in the input assumptions.

There is an interesting collection of papers on Portfolio Optimization at [Worcester Polytechnic Institute](http://www.wpi.edu):

In the next post I will discuss the Black–Litterman model that addresses both Instability and Diversification problems of the portfolios on the mean-variance efficient frontier.

To view the complete source code for this example, please have a look at the [aa.solutions2instability.test() function in aa.test.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/aa.test.r).