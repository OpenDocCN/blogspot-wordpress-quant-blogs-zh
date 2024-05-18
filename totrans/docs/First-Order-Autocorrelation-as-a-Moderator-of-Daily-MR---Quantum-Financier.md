<!--yml
category: 未分类
date: 2024-05-18 14:05:42
-->

# First Order Autocorrelation as a Moderator of Daily MR – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2010/05/07/first-order-autocorrelation-as-a-moderator-of-daily-mr/#0001-01-01](https://quantumfinancier.wordpress.com/2010/05/07/first-order-autocorrelation-as-a-moderator-of-daily-mr/#0001-01-01)

In the same line of thought than my previous post on volatility as a moderator of daily MR, this post will observe first order autocorrelation. From [wiki](http://wikipedia.org/): “Autocorrelation is the cross-correlation of a signal with itself. Informally, it is the similarity between observations as a function of the time separation between them.” Basically, it is the extent to which series values are correlated with previous values (aka lagged values) in the same series. For example, the first order autocorrelation of a daily logarithmic return series is the correlation between two subsets of the return series; the series as is with a look back period and the same subset lagged 1 period.

From a trading perspective, autocorrelation is a very simple tool to incorporate in a market regime indicator, or more globally in a trading system. It is also interesting to see the evolution of autocorrelation in a given asset. The figure below shows the equity curve of the S&P 500 since 1957, the rolling Sharpe ratio of a daily MR strategy (RSI 2 50/50) and finally the first order correlation of the S&P logarithmic return using a rolling 2 years look back period.

[![](img/1fcac83d3058d5e3b1d1b69f27651ccc.png "First order autocorrelation")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/first-order-autocorrelation.jpg)

As one would expect, first order autocorrelation can help moderate daily MR performance. When autocorrelation is positive, daily follow through is more profitable than mean reversion, around the turn of the century however, autocorrelation switched to negative territory, which is consistent with the MR predominance in profitable directional swing strategies as very well explained in the blogs on my blogroll. I plan to post a more number intensive note soon, this was just a post to introduce autocorrelation as a valuable moderator of daily MR.

QF