<!--yml
category: 未分类
date: 2024-05-18 13:47:29
-->

# Proxy Hedging and Dependence | Quantivity

> 来源：[https://quantivity.wordpress.com/2011/10/26/proxy-cross-hedge-correlation-dependence/#0001-01-01](https://quantivity.wordpress.com/2011/10/26/proxy-cross-hedge-correlation-dependence/#0001-01-01)

When asked to summarize their approach to [proxy / cross hedging](https://quantivity.wordpress.com/2011/10/02/proxy-cross-hedging), senior folks from numerous big banks reduced it to correlation: hedge using an instrument whose correlation is close to -1\. This perspective matches the popular practitioner literature, such as recently published text [Hedging Market Exposures](http://books.google.com/books?id=CpSv76NCmJcC) (Bychuk and Haughey, 2011). Moreover, this perspective is at the heart of much of the research literature, going back to original definition of optimal hedge ratio ![\hat{\beta}](img/bf55cafee1613728641a3fb0910e4efd.png) (*e.g.* [Hull](http://books.google.com/books?id=sEmQZoHoJCcC), p. 57):

   ![\hat{\beta} = \rho ( \frac{\sigma_u}{\sigma_h} )](img/30b7f48f8ea271361d9846df5d20f083.png)

Yet, while indeed true, this wisdom is not terribly helpful in practice for hedging well-known equities, as described in previous posts—as no instrument exists with such high correlation. This motivated revisiting the role of dependence in hedging, uncovering what may perhaps be an interesting result: *multi-period asymptotically perfect hedges exist with ![\rho \ll -1](img/e14f50fc2c19ba1275fcec675d240476.png)*.

To derive this result, begin by asking a simple-sounding question: over what range of correlation between underlying and hedge can a perfect hedge conceivably be built? When evaluated for a *single period*, the answer is obviously a single value: ![\rho = -1](img/eacdc8ab71faed0d58e774b80ade78d2.png), as ![\epsilon > 0](img/1fa69ea1fea10840411735cfa4278f5a.png) for any other correlation, given:

   ![\rho \ne -1 \iff u \ne h](img/c4e359f890c687398fa435430f81ab67.png).

Yet, this question becomes more interesting when generalized to *multiple periods*. Specifically, consider the temporal series of proxy errors over multiple contiguous periods:

    ![\{ \epsilon_{t_1}, \epsilon_{t_2}, \dots, \epsilon_{t_n} \} = \boldsymbol{\epsilon}](img/757ee6fcc0a3975439dd60401f794132.png)

Can intuition be built by modeling the temporal evolution of ![\boldsymbol{\epsilon}](img/0853a698c25ab23f3bfd567f6ec6431b.png) directly, rather than describing the characteristics of ![u](img/3e3dc85b695f49b6073b5656627101bb.png) and ![h](img/1aeb683dd8e8cbb4ed875f43ce92850d.png)? Consider modeling ![\boldsymbol{\epsilon}](img/0853a698c25ab23f3bfd567f6ec6431b.png) using elementary trigonometry, say a familiar sin curve:

[![](img/256fa1d9fc834a39d5c726e03764479b.png "proxy-correlation-sin")](https://quantivity.wordpress.com/wp-content/uploads/2011/10/proxy-correlation-sin1.png)

This model is interesting, as it captures the two desirable properties for optimal proxy hedging:

*   **Zero crossings**: error crosses zero a positive number of times during its path (determined by `zerocross` parameter below), providing frequent opportunity to exit hedge with zero loss (*i.e.* ![\boldsymbol{\epsilon} = 0](img/60da9003031e0d7455c0ab3c9571fdb4.png))
*   **Absolute bounds**: error is bounded, above and below, to not exceed some maximum threshold

These two properties should be familiar to readers who trade relative value strategies.

Given the above evolution of ![\boldsymbol{\epsilon}](img/0853a698c25ab23f3bfd567f6ec6431b.png) over time, next question is asking what range of ![\rho](img/3e72a82f16831a4135a859a809b7fe10.png) is possible given arbitrary paths of ![h](img/1aeb683dd8e8cbb4ed875f43ce92850d.png) and ![u](img/3e3dc85b695f49b6073b5656627101bb.png). As always, a picture is worth a thousand words.

Define ![u](img/3e3dc85b695f49b6073b5656627101bb.png) to follow a stochastic process of length ![n](img/4f0c9881324df3a61e8d3cc580ec06e6.png), whose value is drawn from Gaussian (given ![\mu](img/9c754889c3ac09f75741e7f39896143d.png) and ![\sigma](img/527f0b49e7d8291d393b5c36137fd2d0.png) parameters):

```

u <- rnorm(n, mu, sd);

```

In other words, the underlying follows a random process, which seems reasonable. Given that, ![h](img/1aeb683dd8e8cbb4ed875f43ce92850d.png) is determined as the arithmetic difference, given discrete differential of ![\epsilon](img/fa45401b4ac499b260e1f16cdc22b992.png) and desired number of zero crosses for sin curve:

```

e <- (sin(seq(-zerocross*pi, zerocross*pi, len = n)) + 0.01) / 10
de <- diff(e)
h <- de - u

```

The following plots illustrates one sample path of ![u](img/3e3dc85b695f49b6073b5656627101bb.png), with corresponding ![h](img/1aeb683dd8e8cbb4ed875f43ce92850d.png), over the multiple periods (parameters `n=200; zerocross=1; mu=0; sd=0.05`):

[![](img/0602af096a3626ccca858181d02e38e1.png "proxy-correlation-1-returns")](https://quantivity.wordpress.com/wp-content/uploads/2011/10/proxy-correlation-1-returns.png)

These returns look fairly normal, albeit obviously sampled from a distribution which has neither long tails nor memory.

Given underlying and hedge, the correlation density can be generated by sampling ![u](img/3e3dc85b695f49b6073b5656627101bb.png):

```

cor(h, u, method="kendall")

```

The following plots illustrate the simulated scatter and empirical density for ![\rho](img/3e72a82f16831a4135a859a809b7fe10.png), given 1000 iterations (parameters `n=200; zerocross=1; mu=0; sd=0.05`):

[![](img/12e3d29ed0f24666f5fe5513bcd50d36.png "proxy-correlation-1-mc")](https://quantivity.wordpress.com/wp-content/uploads/2011/10/proxy-correlation-1-mc.png)

With a single zero cross, this model recovers the classic one-period optimal hedge result: ![\rho \approx -1](img/ca5c170ff097b68a7dae332f5869d3e2.png).

Where this model becomes interesting is when number of zero crosses is increased above 1\. Doing so diverges the model from classical single period, conceptually extending time over multiple periods. The following plots illustrate returns when zero cross is 10:

[![](img/2d261f4bc5792170dff0568da6351c37.png "proxy-correlation-10-returns")](https://quantivity.wordpress.com/wp-content/uploads/2011/10/proxy-correlation-10-returns.png)

Visual inspection of the cumulative returns plot makes clear something different is afoot. Clearly the underlying and hedge are not behaving as perfect inverses, when there are more zero crosses. There is something deeper at work. To illustrate further, consider the corresponding sampled correlation plots:

[![](img/cc09ed3c0655ddd712c4231628ba928b.png "proxy-correlation-10-mc")](https://quantivity.wordpress.com/wp-content/uploads/2011/10/proxy-correlation-10-mc.png)

Illustrating correlation diverging from -1, peaking near -0.73\. Recall this is correlation of underlying and hedge, which is providing *asymptotic optimality* at a finite number of points in time. Is this an accident, or does it represent a more general principle at work? Consider the following return plots for proxy error with 50 zero crosses:

[![](img/d097b32ecded0f6cc92b3e3fda4dda69.png "proxy-correlation-50-returns")](https://quantivity.wordpress.com/wp-content/uploads/2011/10/proxy-correlation-50-returns.png)

Now the underlying and hedge look nothing like each other, except their broad directions are consistently inverted. Again, consider the corresponding correlation plots, which illustrate sampled correlation decreasing to density peak near -0.30.

[![](img/d2d4b6085952b60bd9cbb2405537414d.png "proxy-correlation-50-mc")](https://quantivity.wordpress.com/wp-content/uploads/2011/10/proxy-correlation-50-mc.png)

This illustrates perhaps an interesting result demonstrating counterexample to the conventional wisdom of perfect negative correlation for proxy hedging, albeit only in theory.

* * *

R code to generate the above sampling and plots:

```

proxyMultiPeriodCorrelation <- function(i=100, zerocross=20, n=200, mu=0, 
                                        sd=0.05, doPlot=FALSE)
{
  # Monte carlo sampling for visualizing multi-period correlation dynamics.
  #
  # Args:
  #     i: number of sampling iterations
  #     zerocross: number of zero crosses for error
  #     n: number of iterations for error sin curve
  #     mu: mean of Gaussian samples for u
  #     sd: standard deviation of Gaussian samples for u
  #     doPlot: flag to indicate whether to plot returns
  #
  # Returns: vector of sampled correlations

  e <- (sin(seq(-zerocross*pi, zerocross*pi, len = n)) + 0.01) / 10
  de <- diff(e)

  cors <- sapply(c(1:i), function(i){ 
    u <- rnorm(length(de),mu,sd); 
    h <- de - u;
    pair <- u + h
    c <- cor(h, u, method="kendall");

    if (doPlot)
    {
      oldpar <- par(mfrow=c(2,1))
      plot(u, type='l', xlab="Time", ylab="Returns", main="Optimal Proxy Returns");
      lines(h, col=colors[2])
      legend("topleft",legend=c("Underlying", "Hedge"), fill=colors, cex=0.5)

      cumH <- cumprod(1+h)-1
      cumU <- cumprod(1+u)-1

      plot(cumU,ylim=c(min(cumH,cumU,e),max(cumH,cumU,e)), type='l', ylab="Cumulative Return", xlab="Time", main="Optimal Proxy Cumulative Returns")
      lines(cumH, col=colors[2])
      lines(e, col=colors[3]);
      legend("topleft",legend=c("Underlying", "Hedge", "Error"), fill=colors, cex=0.5)
      par(oldpar)
    }

    return (c)
  })

  oldpar <- par(mfrow=c(2,1))
  plot(cors, ylab="Correlation", main="Optimal Proxy Hedge Correlation Scatter")
  plot(density(cors), xlab="Correlation", main="Optimal Proxy Hedge Correlation Density")
  par(oldpar)

  return (cors)
}

```