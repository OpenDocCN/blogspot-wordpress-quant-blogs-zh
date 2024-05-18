<!--yml
category: 未分类
date: 2024-05-18 13:54:04
-->

# Paradox of Informedness | Quantivity

> 来源：[https://quantivity.wordpress.com/2010/02/06/paradox-of-informedness/#0001-01-01](https://quantivity.wordpress.com/2010/02/06/paradox-of-informedness/#0001-01-01)

Are the aggregate buy/sell decisions of all traders better than random?

This deceptively simple sounding question has deep, far reaching implications for building quantitative models and high-frequency trading systems. Although many people have speculated on this question for decades, the discipline of [econophysics](http://en.wikipedia.org/wiki/Econophysics) is applying techniques originating from statistical physics (originally [statistical mechanics](http://en.wikipedia.org/wiki/Statistical_mechanics)) to provide insight into this fundamental question.

Econophysics frames this question in the context of *investor informedness*, which is a means of measuring whether the average trade has better than random chance (50/50) to be profitable. Interesting papers in this literature include Fluctuations and Response in Financial Markets by Bouchaud *et al.* and Are Supply and Demand Driving Stock Prices? by Hopman.

Conclusions to this question drawn from experimental high-frequency order/trade analysis are unexpectedly fascinating, and directly result in a *paradox of informedness*:

> The vast majority of trades are empirically proven to be uninformed (meaning they are based upon random buy/sell decisions), yet microstructure models tell us price is determined by the historical sequence of preceding trades. Thus, trades are uninformed, yet form the basis for subsequent price discovery.

In other words, *trades are simultaneously uninformed and informed*. This is deeply unsettling for those (presumably few, given the past two years) believing in rational agents and Efficient Market Hypothesis.

This paradox holds interesting connection to observations from two previous posts:

*   [Causality, Exogeny, and Regimes](https://quantivity.wordpress.com/2010/01/10/causality-exogeny-regimes/): not only are prices not predominantly driven by economic fundamentals, they appear to be driven by rampant uninformed diffusive randomness
*   [Limit Book Simulation](https://quantivity.wordpress.com/2010/01/12/limit-book-simulation/): might the entire market be lulling itself into collective [Jump & Dump](http://www.cdam.lse.ac.uk/Reports/Abstracts/cdam-2005-12.html) behavior writ large (one cannot help but beg the question, given two 30% market swings over the past year)

Given lack of consensus agreement on calculating economic fair value and liquidity providers with intraday time horizons, might 30% prices jumps indeed simply be non-collusive jumping and dumping on a macro timescale?

Bouchaud *et al.* formulates the relationship between historical trades and current prices (*i.e.* inter-trade impact), as follows, where ![G_{0}(l)](img/fe874d95e267111b133e9af4d2726ccd.png) is the average impact of a single trade after ![l](img/f72ec5bdcaec0dbe8f202da71d2765f7.png) subsequent trades:

![p_{n} = \displaystyle\sum_{n' < n} G_{0}(n - n') \epsilon_{n'} \ln V_{n'} + \displaystyle\sum_{n' < n} \eta_{n'}](img/3c8b2271d8fb6d1a4eaf41a6e45429dd.png)

Such inter-trade impact functions only become more fascinating when pondered in the context of the preceding ![(n-1)](img/6ec8f3107cb46c93dc3ee7323a09d70a.png) trades being uninformed.