<!--yml
category: 未分类
date: 2024-05-18 13:51:25
-->

# Minimum Variance Portfolios | Quantivity

> 来源：[https://quantivity.wordpress.com/2011/04/17/minimum-variance-portfolios/#0001-01-01](https://quantivity.wordpress.com/2011/04/17/minimum-variance-portfolios/#0001-01-01)

As recounted in [Portfolio Theory is Dead, Now What?](https://quantivity.wordpress.com/2011/04/10/portfolio-theory-is-dead-now-what/), the *minimum variance portfolio* is the optimal portfolio in a world with zero risk premium. This post expands on the topic via practical implementation in R, preceded by walk through of the corresponding mathematics.

Recall the classic Markowitz mean-variance optimal portfolio is the solution to:

![\begin{aligned}  & \underset{w}{\text{min}}   & &w^{\mathrm{T}} \hat{\Omega} w - \frac{1}{\gamma}  \hat{\mu}^{\mathrm{T}} w \\  & \text{subject to}  & & \sum_i{w_i} = 1, \\  \end{aligned} ](img/c9b2160f9ccba3c66e9aa67b6e760623.png)

where ![w \in \bold{\mathbb{R}^n} ](img/3fbb412f331cdd52dc2b55cbe0c421af.png) are vector of portfolio weights, ![\hat{\mu}^\mathrm{T} w ](img/36fef21bbb2781efc6c3638995f088dd.png) is sample mean portfolio return, and ![w^\mathrm{T} \hat{\Omega} w ](img/567281bcade3c5b41fb93de2199f5123.png) is sample covariance of portfolio returns. The summation to one constraint ensures weight percentages sum to 100%, meaning full investment. An additional common requirement is no short selling (*e.g.* 401k, IRAs, and mutual funds), which adds the following non-negative optimization constraint:

    ![\forall i : w_i \ge 0 ](img/7649415f7339bbaf666591f7b3ed209e.png)

From this starting point, consider two assumptions which lead to the *minimum variance* portfolio:

*   Risk premium is zero
*   Aversion to risk is *infinite*, thus ![\gamma = \infty](img/30624323edc6ec56d8d3d3ad36b4cffa.png)

With those assumptions, the above optimization reduces to the following covariance minimization:

![\begin{aligned}  & \underset{w}{\text{min}}  & &w^\mathrm{T} \hat{\Omega} w \\  & \text{subject to}  & & \sum_i{w_i} = 1, \\  \end{aligned} ](img/374fbdbf7ad08538e7d8568827d15720.png)

For portfolios constructed from individual stocks (as opposed to sectors, for example), an upper bound ![\epsilon ](img/55f2c1da05b6d3e0249335f5aa024a8a.png) constraint on the weights is appropriate to minimize *idiosyncratic* risk:

    ![\forall i : 0 \le w_i < \epsilon. ](img/3d1c152abf8951cefdb2cbe1a252cfac.png)

[Jagannathan and Ma](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=424756) (2002) show this constraint improves estimation by amplifying shrinkage efficacy. The authors demonstrate a similar statistical shrinkage benefit provided by the zero lower bound.

Although this is a rudimentary constrained optimization problem, what makes it fun is the “Markowitz optimization enigma”: robustly estimating the covariance matrix ![\hat{\Omega} ](img/cdb8a4e71da78f087ecbc0f352f72298.png). Consider three estimators from the literature, the first two following [Falkenblog](http://www.betaarbitrage.com/member-equityindices-mvp.php) and [Estimation Risk](http://estimationrisk.blogspot.com/) and the final being a more recent estimator. All estimators ensure the covariance matrix is [positive definite](http://en.wikipedia.org/wiki/Positive-definite_matrix) (as required to ensure the optimization is [convex](http://en.wikipedia.org/wiki/Convex_optimization)).

*   **Asymptotic Components with Hetersokedastic Factor Residuals**

Following Falkenstein, use Connor and Korajczyk (1993) and Jones (2001) to estimate ![\hat{\Omega} ](img/cdb8a4e71da78f087ecbc0f352f72298.png):

   ![\hat{\Omega} = B^\mathrm{T} (F F^\mathrm{T}) B ](img/db4122aae91a48f9352c75cedc524e95.png)
   ![B = (F F^\mathrm{T})^{-1} (F R^\mathrm{T}) ](img/7aa34795819fe8a8cb86cc063e4ecec1.png)

Where ![R](img/e9185405078a808ad045a6921814a68b.png) (![N \times T](img/a8e5133899e2869a7afb6f69e0826cc1.png)) is historical returns for T periods on N instruments and ![F](img/19221831632e5c3c0d42a97235b400cf.png) (![T \times K](img/ebd84edbdf69f25faff126b022387bbd.png)) are the Jones factors.

*   **Bayesian Sample Shrinkage Estimator**

Similar to Nogales, use Ledoit and Wolf (2004) to estimate ![\hat{\Omega} ](img/cdb8a4e71da78f087ecbc0f352f72298.png) via [shrinkage](http://en.wikipedia.org/wiki/Shrinkage_estimator) with a Bayesian prior and sample covariance matrix:

    ![\hat{\Omega} = \hat{\delta} F + (1 - \hat{\delta})S](img/aa0c1c2e557b982a7bbf6ab5e34d3d21.png)
    ![\hat{\delta} = \max(0, \min(\frac{\hat{\kappa}}{T}, 1))](img/0200d2f767f3110e53384a42fb067d6d.png)
    ![\hat{\kappa} = \frac{\hat{\pi} - \hat{\phi}}{\hat{\gamma}}](img/ed3444021373be19cf294810aac91955.png)

where ![T](img/b176bdc7d12e2bd6122b89261ffbf2d8.png) is length of time-series, ![S ](img/691c8c17be9ffe6431f6a944fee6c4e4.png) is the sample covariance matrix, ![\hat{\delta} ](img/a82c8980ab06f5f4dbf2fb750c6b75ae.png) is the shrinkage constant, and the elements of the estimator ![F](img/19221831632e5c3c0d42a97235b400cf.png) are composed:

    ![f_{ii} = s_{ii} : \forall i](img/2944fc0f5546e50bd0107939945a5368.png)
    ![f_{ij} = \bar{r} \sqrt{s_{ii}s_{jj}} : \forall i \neq j ](img/3abfd7ff7eb410d21211348ec86feba9.png)

*   **Sample Variance and Correlation Shrinkage Estimator**

Following Schäfer and Strimmer (2005) and Opgen-Rhein and Strimmer (2007) to estimate ![\hat{\Omega} ](img/cdb8a4e71da78f087ecbc0f352f72298.png) via [shrinkage](http://en.wikipedia.org/wiki/Shrinkage_estimator) of both variance and correlation:

    ![\hat{s}_{kl} = \hat{r}_{kl} \sqrt{\hat{v_k}\hat{v_l}} ](img/cecba25c40a03bf7e969f31d67be457a.png)
    ![\hat{r}_{kl} = (1 - \hat{\lambda_1}) r_{kl} ](img/5aa2d47dda0c18537ba1797b3c7c6577.png)
    ![\hat{v_k} = \hat{\lambda_2}v_{\mathrm{median}} + (1 - \hat{\lambda_2}) v_k ](img/292e123bcfbcc1da71d805fbb3efb206.png)
    ![\hat{\lambda_1} = \min(1, \frac{\sum\limits_{k \neq l} \hat{var}(r_{kl})}{\sum\limits_{k \neq l} r^2_{kl}}) ](img/a7de7cbb2368a083434b15a6ffba3084.png)
    ![\hat{\lambda_2} = \min(1, \frac{\sum\limits_{k=1}^p \hat{var}(v_k)}{\sum\limits_{k=1}^p (v_k - v_{\mathrm{median}})^2}) ](img/1e3c0f0b55e233480b2a5db07155a4b1.png)

* * *

Now consider the R necessary to generate these portfolios. Readers seeking more background on portfolio optimization in R are referred to [R Tools for Portfolio Optimization](http://www.rinfinance.com/RinFinance2009/presentations/yollin_slides.pdf) by Yollin (R/Finance 2009).

The most important detail is choice of covariance estimator, including Schäfer-Strimmer-Opgen-Rhein from [`corpcor`](http://cran.r-project.org/web/packages/corpcor/) package and Ledoit-Wolf from [`tawny`](http://cran.r-project.org/web/packages/tawny/index.html) package (both functions confusingly named `cov.shrink`). The Ledoit-Wolf estimator will be used in this and subsequent posts.

These optimizations can be formulated as quadratic programming, and solved using `solve.QP` from `quadprog`, via formulating the above optimizations into the following functional form (following [Goldfarb and Idnani](http://www.javaquant.net/papers/GoldfarbIdnani.pdf) (1982, 1983)) with a zero ![d^\mathrm{T}](img/f40c1bc5dfa5151c456a53d302225dad.png):

![\begin{aligned}  & \underset{b}{\text{min}}   & & \frac{1}{2} b^{\mathrm{T}} D b - d^{\mathrm{T}} b \\  & \text{subject to}  & & A^{\mathrm{T}} b \ge b_0  \end{aligned} ](img/bdcfbe6bb337911b41c2e4d9668ed12f.png)

Assume `X` is a matrix of log returns, then generate optimization inputs:

```

<code>covar <- cov.shrink(X)
N <- ncol(X)
zeros <- array(0, dim = c(N,1))

```

Evaluate the optimization to generate minimum variance portfolio without short selling constraint:

```

aMat  <- t(array(1, dim = c(1,N)))
res <- solve.QP(covar, zeros, aMat, bvec=1, meq = 1)

```

Or, similar optimization with short selling constraint (*i.e.* non-negative weights):

```

aMat <- cbind(t(array(1, dim = c(1,N))), diag(N))
b0 <- as.matrix(c(1, rep.int(0,N)))
res <- solve.QP(covar, zeros, aMat, bvec=b0, meq = 1)

```

Finally, return portfolio attributes (similar to `portfolio.optim`):

```

y <- X %*% res$solution
port <- list(pw = round(res$solution,3), px = y, pm = mean(y), ps = sd(y))

```

One minor numerical analysis reminder: use of `solve.QP` with short selling constraints may generate weights with a negative sign (*e.g.* `-3.417223e-17`), due to floating point precision and numerical stability. Such weights are equal to zero when rounded to a reasonable number of digits.

A subsequent post will apply these minimum variance optimization to building and evaluating risk for rotation strategies.