<!--yml
category: 未分类
date: 2024-05-18 13:55:55
-->

# Naïve Backtesting is Bogus | Quantivity

> 来源：[https://quantivity.wordpress.com/2009/08/16/naive-backtesting-is-bogus/#0001-01-01](https://quantivity.wordpress.com/2009/08/16/naive-backtesting-is-bogus/#0001-01-01)

The most frequently cited [conventional wisdom](http://en.wikipedia.org/wiki/Conventional_wisdom) of quant trading is backtesting, often summarized as:

> Wise traders do as much [backtesting](http://en.wikipedia.org/wiki/Backtesting) as possible before starting to trade a system with real money.

Unfortunately, this wisdom is bogus. More accurately, this *wisdom is bogus when practiced according to the standard backtesting formula*:

1.  Indicator: choose indicator (whether fundamental, technical, or statistical)
2.  Data: choose long panel of data for some instrument (usually as much data as possible)
3.  Backtest: build strategy by optimizing entry and exit, given indicator, over data panel
4.  Profit!

Yes, undoubtedly some traders find short-term success with this formula. This is actually inevitable, due to the [infinite monkey theorem](http://en.wikipedia.org/wiki/Infinite_monkey_theorem): enough traders doing enough [data snooping](http://en.wikipedia.org/wiki/Data-snooping_bias) on powerful computers will inevitably result in a small number of them discovering what appears to be successful strategy due to pure randomness.

Consider an automotive analogy, to help illustrate the fallacy of this formula: predict the future [viscosity](http://en.wikipedia.org/wiki/Viscosity) of oil, given many measurements of viscosity at random times over a preceding period of time. Such measurements exhibit the following statistical attributes:

*   Random dispersion: values appear randomly, roughly following [Brownian motion](http://en.wikipedia.org/wiki/Brownian_motion)
*   Two primary clusters: values appear roughly centered around two primary [clusters](http://en.wikipedia.org/wiki/Cluster_analysis)
*   Random outliers: random outliers exist between the two primary clusters, mostly lying on the plane connecting the two clusters

These measurements very roughly follow what traders observe in low-frequency security prices (oil in above analogy) across bull/bear market regimes (cluster in above analogy). Given that, back to prediction: what will future values of viscosity be given the past? Many years of effort could go into analyzing this problem, with numerous results providing mild predictiveness gained from use of diverse applied mathematical methods. Readers are encouraged to ponder this challenge, assuming they are given no more data than above.

Much of quant trading is analagous to this viscosity problem: blindly backtesting over myriad observed measurements, rigorously optimizing parameters using varying mathematical methods.

Now, consider one additional fact being discovered: oil being measured is contained in an engine, which randomly varies between being “on” and “off” for periods of time. With this knowledge (knowing running engines are hot), quants will quickly recall the relationship between temperature and viscosity. Shortly thereafter, someone will combine [Sutherland’s formula](http://en.wikipedia.org/wiki/Viscosity#Effect_of_temperature_on_the_viscosity_of_a_gas) with [cluster analysis](http://en.wikipedia.org/wiki/Cluster_analysis) and identify an effective prediction methodology.

If traders have learned anything during either 2007 – 2009 (or 1998 – 2002), it should be that the fundamentals of economics and finance are not stable: *nearly every statistical measure in common use across nearly all asset classes exhibited inconsistent behavior over this period* (mean, variance, volatility, covariance, correlation, cointegration, principal components, skew, kurtosis, *etc*.). Introductory economics informs us the root causes for these instabilities are many, ranging from [business cycles](http://en.wikipedia.org/wiki/Business_cycle) to [monetary policy](http://en.wikipedia.org/wiki/Monetary_policy).

Yet, despite these first-hand observations, many traders merrily go along their way continuing to faithfully believe in the wisdom of backtesting. By the above analogy, traders would benefit from refining their quantitative methodologies to accommodate systemic biases—rather than blindly backtesting over long periods of time, with no concern for [externalities](http://en.wikipedia.org/wiki/Externality) such as market regime.

The real challenge is *somehow refining the methodology of quantitative trading in response to this knowledge*. Subsequent posts will strive to take up this challenge, with hope readers contribute their expertise.