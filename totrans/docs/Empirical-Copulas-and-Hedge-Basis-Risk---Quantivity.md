<!--yml
category: 未分类
date: 2024-05-18 13:48:18
-->

# Empirical Copulas and Hedge Basis Risk | Quantivity

> 来源：[https://quantivity.wordpress.com/2011/10/10/empirical-copulas-and-proxy-cross-hedge-basis-risk/#0001-01-01](https://quantivity.wordpress.com/2011/10/10/empirical-copulas-and-proxy-cross-hedge-basis-risk/#0001-01-01)

The recently introduced [proxy hedge model](https://quantivity.wordpress.com/2011/10/02/proxy-cross-hedging) and corresponding [empirical proxy quantiles](https://quantivity.wordpress.com/2011/10/03/empirical-quantiles-proxy-cross-hedging-selection) share an implicit dependence on the *joint covariation* between underlying and proxy hedge. Of particular interest is understanding the dynamics of *basis risk* under extreme scenarios (both up and down), which are driven by time-varying stochastic joint covariation.

This post quantifies and visualizes such joint covariation and basis risk via [copulas](http://en.wikipedia.org/wiki/Copula_%28probability_theory%29), including modeling and empirically fitting both marginal and joint distributions using fat-tailed [student-t](http://en.wikipedia.org/wiki/Student%27s_t-distribution) distributions. Copulas exploit multidimensional sample ranking, and thus are thematically similar to empirical quantiles. This analysis also seeks to exemplify practical use of R for copula analysis.

Brief review of the shortcomings of classic [dependence statistics](http://en.wikipedia.org/wiki/Correlation_and_dependence) (such as correlation and covariance) motivates use of copulas and related techniques:

*   **Normality**: assumption of joint normality in one guise or another, irrespective of suitability
*   **Summary statistics**: [point estimates](http://en.wikipedia.org/wiki/Point_estimation) which reduce complex covariation relationships into single numbers
*   **Marginal-joint conflation**: considerations of both marginal and joint are conflated, rather than providing clean and independent separation
*   **Poor visualization**: few visualization techniques exist, reducing potential for geometric and topological intuition

These shortcomings were resolved by the following beautiful decomposition, due to [Sklar (1959)](http://www.jstor.org/pss/4355880):

   ![H(x, y) = C( F(x), G(y) ) ](img/14796f71fb68d0c41f47febda1029010.png)

where ![F](img/19221831632e5c3c0d42a97235b400cf.png) and ![G](img/50c45590b30932e6c16cbbc26766322b.png) are univariate distributions, ![H](img/08f86bb6e2072ba520c148934f76c0bf.png) is a two-dimensional distribution function with marginal distributions ![F](img/19221831632e5c3c0d42a97235b400cf.png) and ![G](img/50c45590b30932e6c16cbbc26766322b.png), and ![C](img/e5cf91abc25ecaf404555860373f6acc.png) is a copula. Note that any or all of ![F](img/19221831632e5c3c0d42a97235b400cf.png), ![G](img/50c45590b30932e6c16cbbc26766322b.png), and ![C](img/e5cf91abc25ecaf404555860373f6acc.png) may be fitted empirically. [Trivedi and Zimmer (2005)](http://http://bit.ly/pMjQR4) or [Cherubini *et al.* (2004)](http://books.google.com/books?id=0dyagVg20XQC) are suggested for readers unfamiliar with copulas.

Conceptually, this technique provides several useful benefits for analyzing proxy hedging basis risk:

*   **Mechanics**: Any joint distribution can be bi-directionally “glued together” by two marginals and a copula
*   **Uniqueness**: Copula is unique, under conditions reasonable for current purposes
*   **Completeness**: Joint covariation can be fully characterized by a copula, independent from the marginals
*   **Visualization**: Copulas can graphically visualized, in both contours and density plots

Without further ado, the following plots visualize the daily joint covariation of well-known tech stock and QQQ linear returns over the longitudinal period via an *empirical proxy copula* (1254 daily observations), as introduced in [Empirical Quantiles and Proxy Selection](https://quantivity.wordpress.com/2011/10/03/empirical-quantiles-proxy-cross-hedging-selection). Note these plots illustrate *joint covariation independent from the marginal densities* of CRM / QQQ:

[![Proxy Copula Summary](img/043619b48e4d530b9279c14a7cb70603.png "proxy-copula-all")](https://quantivity.wordpress.com/wp-content/uploads/2011/10/proxy-copula-all2.png)

The top left plot illustrates scatter of ranked pseudo observations; top right illustrates scatter of 1000 random samples from the fitted copula; bottom left illustrates empirical copula contour; and bottom right illustrates the empirical copula perspective. Compare this diversity of visualization versus a single number (*e.g.* correlation statistic, which happens to equal `0.777`).

Diving into the marginal and copula distribution is necessary to understand this relationship further. Consistent with standard convention, all distributions are assumed to be student-t with empirically fitted degrees of freedom. The parameters of the marginals are:

`CRM location 0.0003 scale 0.0218 df 3.489
QQQ location 0.001 scale 0.0100 df 2.767`

Indicating the marginal distributions diverge strongly from normality with fat trails, due to small degrees of freedom. This matches the 3 df estimate by Schoeffel in his [recent (2011) article](http://arxiv.org/abs/1110.1006) on futures (note difference in frequency and log returns).

Similarly, the copula is assumed to be distributed student-t with estimated df of `3.975` and ![\rho](img/3e72a82f16831a4135a859a809b7fe10.png) of `0.6868`. The bivariate association measures for the empirical proxy copula are:

`tau 0.481
rho 0.669
tail index: 0.381 0.381`

Indicating the copula also strongly diverges from normality with strongly fat tails.

In summary: these plots and fitted distributions confirm observed conclusions from the [previous post](https://quantivity.wordpress.com/2011/10/03/empirical-quantiles-proxy-cross-hedging-selection): although CRM and QQQ covary, there is *high basis risk*—including numerous observations with nearly inverse correlation. In other words, a QQQ proxy is likely to result in fairly costly hedging errors.

* * *

R code to generate the above empirical proxy copula analysis (and more, possibly to be covered in a subsequent post):

```

require("copula")
require("fSeries")

exploreProxyDist <- function(p, doExcess=TRUE, partitions=1)
{
  # Analyze distribution and copula of proxy daily returns.
  #
  # Args:
  #   p: matrix of instrument price data, including valid colnames
  #   doExcess: flag indicating whether to perform analysis on excess returns, 
  #             in addition to raw returns
  #   partitions: if not 1, partition the returns and perform subanalysis
  #
  # Returns: None

  oldpar <- par(mfrow=c(2,2))
  n <- nrow(p)

  # first differences (not logged)
  pROC <- ROC(p, type="discrete", na.pad=FALSE)
  exploreProxyDistROC(pROC)

  if (partitions > 1)
  {
    frac <- floor(n / partitions)
    sapply(c(0:(partitions-1)), function(p) { cat("\n",
                                                (p+1),"-th partition:",((p*frac)+1), 
                                                ((p+1)*frac),"\n"); 
                                                partition <- pROC[((p*frac)+1):((p+1)*frac),]
                                                exploreProxyDistROC(partition) } )
  }

  if (doExcess)
  {
    cat("\nExcess Copula\n")

    # calculate excess returns, subtracting off market
    excess <- pROC[,1] - pROC[,2]
    excessROC <- cbind(excess, pROC[,2])

    par(oldpar)
    plot(cumprod(1+excess), main="Excess Cumulative Returns", ylab="Return")
    oldpar <- par(mfrow=c(2,2))

    exploreProxyDistROC(excessROC)

    if (partitions > 1)
    {
      frac <- floor(n / partitions)
      sapply(c(0:(partitions-1)), function(p) { cat("\n",
                                                  (p+1),"-th Excess Partition:",((p*frac)+1), 
                                                  ((p+1)*frac),"\n"); 
                                                  partition  <- excessROC[((p*frac)+1):((p+1)*frac),]
                                                  exploreProxyDistROC(partition) } )
    }
  }

  par(oldpar)
}

exploreProxyDistROC <- function(pROC)
{
  # Analyze distribution and copula of proxy daily returns.
  #
  # Args:
  #   p: matrix of instrument price data, including valid colnames
  #
  # Returns: list of copula fit and empirical copula

  n <- nrow(pROC)
  cnames <- colnames(pROC)

  # t-distribution fits
  p1Fit <- fitdistr(pROC[,1], "t")$estimate
  p2Fit <- fitdistr(pROC[,2], "t")$estimate

  cat(cnames[1], "location", p1Fit[1], "scale", p1Fit[2], "df", p1Fit[3], "\n")
  cat(cnames[2], "location", p2Fit[1], "scale", p2Fit[2], "df", p2Fit[3], "\n")

  # empirical copula
  tau <- cor(pROC, method="kendall")[2]
  t.cop <- tCopula(tau, dim=2, dispstr="un", df=3)
  psuedo <- apply(pROC, 2, rank) / (n + 1)
  plot(psuedo, main="Empirical Scatterplot", xlab=cnames[1], ylab=cnames[2])

  fit.mpl <- fitCopula(t.cop, psuedo, method="mpl", estimate.variance=FALSE)
  print(fit.mpl)

  # build empirical copula and plot
  empiricalCopula <- tCopula(fit.mpl@estimate[1], dim=2, dispstr="un", df=fit.mpl@estimate[2])
  plot(rcopula(empiricalCopula, 1000), main="Sampled Scatterplot", xlab=cnames[1], ylab=cnames[2])
  contour(empiricalCopula, pcopula, main="Empirical Contour", xlab=cnames[1], ylab=cnames[2])
  persp(empiricalCopula, dcopula, main="Empirical Perspective",
    xlab=cnames[1], ylab=cnames[2], zlab="Density")

  cat("Empirical tau:", kendallsTau(empiricalCopula), "\n")
  cat("Empirical rho:", spearmansRho(empiricalCopula), "\n")
  cat("Empirical tail index:", tailIndex(empiricalCopula), "\n")

  return (list(fit=fit.mpl, copula=empiricalCopula))
}

```