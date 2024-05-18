<!--yml
category: 未分类
date: 2024-05-18 13:46:26
-->

# Return Decomposition via Mixing | Quantivity

> 来源：[https://quantivity.wordpress.com/2011/12/28/estimating-mixture-index-return-decomposition-via-maximum-likelihood/#0001-01-01](https://quantivity.wordpress.com/2011/12/28/estimating-mixture-index-return-decomposition-via-maximum-likelihood/#0001-01-01)

A variety of techniques exist for estimating parameters of the return decomposition model, previously introduced in [Index Return Decomposition](https://quantivity.wordpress.com/2011/12/14/index-return-decomposition/). This post considers estimation of an *independent mixture model* via maximum likelihood (MLE), a workhorse of frequentist statistics and always a nice place to begin.

Recall ![z](img/7d74f7d8fdd6545e22c6dd9de0af53b3.png) is *unobserved*, and thus the model cannot be directly estimated via MLE. Thus, need to decide how to approach estimation for this latent variable. One way is to be naive, and simply assume ![z](img/7d74f7d8fdd6545e22c6dd9de0af53b3.png) is the deterministic difference in return between stock and index (technically, this generates a [profile likelihood](http://en.wikipedia.org/wiki/Likelihood_function#Profile_likelihood) as formalized by [Severini and Wong [1992]](http://people.csail.mit.edu/~jrennie/trg/papers/severini-conditionally-92.pdf), which [Murphy and Van Der Vaart [2000]](http://www.jstor.org/pss/2669386) verify is well-behaved consistent with exact likelihood):

   ![z_t = r_t - i_t ](img/9406f569aca4e251c598dbe26d85eef1.png)

This assumption permits focus on estimating ![\alpha](img/9a53e012ad26523af8c1a6778d340c3f.png), providing insight into the *mixing behavior* of the return being decomposed: if a stock return behaves like its index, then mixing is low with small ![\alpha](img/9a53e012ad26523af8c1a6778d340c3f.png) (in the limit, ![\alpha = 0](img/52b5c00309e065e19db837bc8b91a752.png) when a stock behaves identical to its index, as no mixing is required); in contrast, the stock return behaves independent from its index on a regular basis, then mixing is high with a large ![\alpha](img/9a53e012ad26523af8c1a6778d340c3f.png).

Autocorrelation of ![i](img/6aed483d693a0743f647c27ec4372c2a.png) and ![z](img/7d74f7d8fdd6545e22c6dd9de0af53b3.png) is worth consideration, as that helps determine whether time indexing is required for ![\alpha](img/9a53e012ad26523af8c1a6778d340c3f.png). For returns with insignificant autocorrelation (common for *signed* equity returns), the time index is dropped and a single ![\alpha](img/9a53e012ad26523af8c1a6778d340c3f.png) is estimated. Yet, *conditional dependence* often exists between ![i](img/6aed483d693a0743f647c27ec4372c2a.png) and ![z](img/7d74f7d8fdd6545e22c6dd9de0af53b3.png), consistent with previous posts in the [Proxy / Cross Hedging](https://quantivity.wordpress.com/2011/10/02/proxy-cross-hedging/) series (illustrating r-z copula for CRM / QQQ example below):

[![](img/d52a149560df398f8f8a27d96db1a5c4.png "z-r-empirical-copula")](https://quantivity.wordpress.com/wp-content/uploads/2011/12/z-r-empirical-copula.png)

Use of this identity for ![z_i](img/1088d8d1a22a00dc3cf8fd0af3dbde55.png) transforms the decomposition model into:

   ![r_t = s_t \left[ \alpha_t | (r_t - i_t) | + (1 - \alpha_t) \beta | i_t | \right] ](img/f32c42b7f1f93f3ffdcab23e1872b887.png)

The model is further simplified into a familiar *independent mixture model* by dropping sign ![s_t](img/3d34b6bd645c53954926164c36a40ae9.png) and ![\beta](img/e59dd600f7eb22f952e355797bceba2e.png), and estimating via MLE using density ![f](img/f6f5c905b764a946a65bee80b6736fe6.png) and return distribution functions ![\phi_i](img/be9f6c685169bb91b421eb34dc9abdb4.png):

   ![f(r_t; \boldsymbol{\theta}) = \alpha \phi_1(r_t - i_t) + (1 - \alpha) \phi_2(i_t)  ](img/4882ebdb6e48051d820ea02018a5f2f1.png)

MLE estimation requires assumption of parametric distributions for ![\phi_i](img/be9f6c685169bb91b421eb34dc9abdb4.png), of which common choices from the literature are normal, student-t, skew-t, or skew hyperbolic student-t ([Aas and Haff [2006]](http://www.econ.ku.dk/fru/conference/Programme/Sunday/F4/Aas_226.pdf)). Next question is how to estimate the ![\boldsymbol{\theta}](img/fd899b1331662dd5d038aff6ddde37b9.png) parameters: ![\alpha](img/9a53e012ad26523af8c1a6778d340c3f.png) and family of ![\phi_i](img/be9f6c685169bb91b421eb34dc9abdb4.png) parameters (*e.g.* ![\mu_i](img/9840e9175f3add00a2433beec43402e8.png) and ![\sigma_i](img/63292fcbee22336be0cef01660cacbe6.png) if ![\phi_i](img/be9f6c685169bb91b421eb34dc9abdb4.png) is assumed to be normal). As ![i_t](img/d1ba04e50950b99d9eabd6f208278285.png) is observed, one way to proceed is via two-step estimation:

1.  Estimate ![\phi_2](img/99322676b5ef63b1e34f31e85ad3be1b.png) parameters via MLE from ![i_t](img/d1ba04e50950b99d9eabd6f208278285.png)
2.  Jointly estimate ![\alpha](img/9a53e012ad26523af8c1a6778d340c3f.png) and ![\phi_1](img/bc97634b37bdf282a3d4ff84cec42357.png) parameters via MLE on the mixture, holding ![\phi_2](img/99322676b5ef63b1e34f31e85ad3be1b.png) parameters constant

For both, recall the likelihood ![\mathcal{L} ](img/8639f7e55dad758d20f029b786e751d6.png), and log likelihood ![ln \mathcal{L} ](img/4c1a27f1b1e4e4bbf2a5638e366df39a.png), are defined as:

   ![\mathcal{L} = \prod\limits_{t=1}^T f(r_t; \boldsymbol{\theta}) ](img/69dd76d6496656f37973a0ce3b9e18d5.png)

   ![\ln \mathcal{L} = \sum\limits_{t=1}^T \ln f(r_t; \boldsymbol{\theta}) ](img/7eed25417f5e550d7141b12079f83278.png)

From which MLE of the mixture is maximization of the likelihood over ![\boldsymbol{\theta}](img/fd899b1331662dd5d038aff6ddde37b9.png), where log is chosen for numeric stability:

   ![\displaystyle \max_{\boldsymbol{\theta}} \ln \mathcal{L} = \max_{\boldsymbol{\theta}} \sum\limits_{t=1}^T \left( \ln \left[ \alpha (r_t - i_t) + (1 - \alpha) i_t \right] \right)](img/cdf953d7d59bf32767f8f0679d0f2692.png)

This optimization can be performed numerically in R via minimization using `DEoptim` of the negative log likelihood `negLogLikeFun` (negative is due to minimization in `DEoptim` versus maximization of ![\ln \mathcal{L}](img/4967bf980eb26ee995662054c8a70def.png)). `DEoptim` is chosen due to rapid convergence on non-smooth global optimizations.

For example, continuing the example of CRM / QQQ introduced in the previous posts on [Proxy / Cross Hedging](https://quantivity.wordpress.com/2011/10/02/proxy-cross-hedging/) generates the results:

```

> symbols <- c("CRM", "QQQ")
> endDate <- Sys.Date()
> startDate <- endDate - as.difftime(52*5, unit="weeks")
> quoteType <- "Close"
> p <- do.call(cbind, lapply(symbols, get.hist.quote, start=startDate, end=endDate,  quote=quoteType))
> colnames(p) <- symbols
> doReturnDecomp(p)
normal mix likelihood: -3485.55 phi1 params: 0.0003471366 0.01673634 params 0.2546208 -0.001208877 0.0113988
skew-t mix likelihood: -3566.512 phi1 params: 0.003844969 0.01079941 -0.3252923 2.893228 params 0.2357737 -0.004188977 0.01099266 0.4157174 26.5643
skew-hyp-t likelihood: -3083.700 phi1 params: 0.01051675 0.1485529 -3.945452 10.10836 params 0.8295289 -0.0003636940 0.03071332 -0.5 5

```

These results correspond to the following density functions for the skew-t mixture:

[![](img/bd68b0d9020342a45209d7d160be8274.png "return-decomp-mixture-densities-skewt")](https://quantivity.wordpress.com/wp-content/uploads/2011/12/return-decomp-mixture-densities-skewt2.png)

One interesting observation of these densities is their location parameters are on opposing side of zero: ![z](img/7d74f7d8fdd6545e22c6dd9de0af53b3.png) has positive location, while ![i](img/6aed483d693a0743f647c27ec4372c2a.png) has negative location. One interpretation of this is positive returns from CRM disproportionately originate from the idiosyncratic ![z_t](img/74d890ac7e079882a239837ea3afdf8c.png), while negative returns originate from the index ![i_t](img/d1ba04e50950b99d9eabd6f208278285.png). Economically, this is plausible: positive news is often idiosyncratic, while negative news is often market-wide.

Several additional inferences can be drawn from these results:

*   Model selection: likelihood suggests skew-t is the preferred model, indicating long tails and skewness (matching stylized facts)
*   Mixing: ![\alpha = 0.24](img/2ba46f580ddd22c68f4055ca912bb243.png) indicating that over 75% of CRM returns are determined by the corresponding QQQ index; remaining 25% are determined by the unobserved ![z](img/7d74f7d8fdd6545e22c6dd9de0af53b3.png) return series
*   Tails: CRM ![\phi_1](img/bc97634b37bdf282a3d4ff84cec42357.png) df = 2.89 which indicates significantly thicker tails than QQQ ![\phi_2](img/99322676b5ef63b1e34f31e85ad3be1b.png) df = 26.56 (matching stylized facts for individual stocks versus indices)

Subsequent posts may consider alternative estimation techniques for this model.

* * *

R code for generating two-stage MLE estimation of return decomposition via mixing:

```

library("MASS")
library("stats")
library("DEoptim")
library("sn")
library("SkewHyperbolic")

normalMixtureIndexDecomp <- function(r, i)
{
  # Two-step MLE estimation of return decomposition model, assuming both
  # return distributions are normal.
  #
  # Args:
  #   r: return series being decomposed
  #   i: index series used for decomposition
  #
  # Return value: MLE parameter estimates

  z <- r - i
  id <- fitdistr(i, "normal")$estimate
  negLogLikeFun <- function(p) {
    a <- p[1]; mu1 <- p[2]; s1 <- p[3];
    ll <- (-sum(log(a * dnorm(z,mu1,s1) + (1 - a) * dnorm(i, id[1], id[2]))));
    return (ll); 
  }
  mle <- DEoptim(negLogLikeFun, c(0, -0.5, 0), c(1, .5, .5), control=list(trace=FALSE))

  cat("normal mix likelihood:", last(mle$member$bestvalit), "phi1 params:",id, "params", last(mle$member$bestmemit),"\n")
  mle <- last(mle$member$bestmemit)

  x <- seq(-.25,.25,length.out=500)
  dnorm1 <- dnorm(x, id[1], id[2])
  dnorm2 <- dst(x, mle[2], mle[3])
  plot(x, dnorm1, type='l', ylim=c(0, max(dnorm1,dnorm2)), ylab="Density", main="Normal Mixture")
  lines(x, dnorm2, col='red')
  abline(v=id[1], lty=2)
  abline(v=mle[2], col='red', lty=2)
  legend("topleft",legend=c("phi1", "phi2"), fill=colors, cex=0.5)

  return (mle)
}

mixtureSkewTIndexDecomp <- function(r, i)
{
  # Two-step MLE estimation of return decomposition model, assuming both
  # return distributions are skew-t.
  #
  # Args:
  #   r: return series being decomposed
  #   i: index series used for decomposition
  #
  # Return value: MLE parameter estimates

  z <- r - i
  idp <- st.mle(y=i)$dp
  negLogLikeFun <- function(p) {
    a <- p[1]; mu1 <- p[2]; s1 <- p[3]; s2 <- p[4]; df1 <- p[5]
    ll <- (-sum(log(a * dst(z,location=mu1,scale=s1,shape=s2,df=df1) + (1 - a) * dst(i, dp=idp))));
    return (ll); 
  }
  mle <- DEoptim(negLogLikeFun, c(0, -0.5, 0, 0, 2), c(1, .5, .5, 5, 50), control=list(trace=FALSE))

  cat("skew-t mix likelihood:", last(mle$member$bestvalit), "phi1 params:", idp, "params", last(mle$member$bestmemit),"\n")
  mle <- last(mle$member$bestmemit)

  x <- seq(-.25,.25,length.out=500)
  dst1 <- dst(x, dp=idp)
  dst2 <- dst(x, dp=mle[2:5])
  plot(x, dst1, type='l', ylim=c(0, max(dst1,dst2)), ylab="Density", main="Skew T Mixture")
  lines(x, dst2, col='red')
  abline(v=idp[1], lty=2)
  abline(v=mle[2], col='red', lty=2)
  legend("topleft",legend=c("phi1", "phi2"), fill=colors, cex=0.5)

  return (mle)
}

mixtureSkewHypTIndexDecomp <- function(r, i)
{
  # Two-step MLE estimation of return decomposition model, assuming both
  # return distributions are skew hyperbolic student-t.
  #
  # Args:
  #   r: return series being decomposed
  #   i: index series used for decomposition
  #
  # Return value: MLE parameter estimates

  z <- r - i
  iparam <- skewhypFit(i,plots=FALSE,printOut=FALSE)$param
  negLogLikeFun <- function(p) {
    a <- p[1];
    ll <- (-sum(log(a * dskewhyp(z,param=p[2:5]) + (1 - a) * dskewhyp(i, param=iparam))));
    return (ll); 
  }
  mle <- DEoptim(negLogLikeFun, c(0, -5, 0, -0.5, 0), c(1, 5, .5, -0.5, 5), control=list(trace=FALSE))

  cat("skew-hyp-t likelihood:", last(mle$member$bestvalit), "phi1 params:",iparam,"params", last(mle$member$bestmemit),"\n")
  mle <- last(mle$member$bestmemit)

  x <- seq(-.25,.25,length.out=500)
  dskewhyp1 <- dskewhyp(x, param=iparam)
  dskewhyp2 <- dskewhyp(x, param=mle[2:5])
  plot(x, dskewhyp1, type='l', ylim=c(0, max(dskewhyp1,dskewhyp2)), ylab="Density", main="Skew Hyperbolic Student-T")
  lines(x, dskewhyp2, col='red')
  abline(v=iparam[1], lty=2)
  abline(v=mle[2], col='red', lty=2)
  legend("topleft",legend=c("phi1", "phi2"), fill=colors, cex=0.5)

  return (mle)
}

doReturnDecomp <- function(p)
{
  # Decompose return of two series, using several parametric distributions.
  #
  # Args:
  #   p: p[,1] is return being decomposed; p[,2] is index returns
  #
  # Return value: none

  r <- ROC(p[,1], type="discrete", na.pad=FALSE)
  i <- ROC(p[,2], type="discrete", na.pad=FALSE)

  normalMixtureIndexDecomp(r, i)
  mixtureSkewTIndexDecomp(r,i)
  mixtureSkewHypTIndexDecomp(r,i)
}

```