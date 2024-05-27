<!--yml

分类：未分类

日期：2024-05-18 04:46:05

-->

# Intelligent Trading: Modified Donchian Band Trend Follower using R, Quantmod, TTR -Part 2: Parameter Sweep Sensitivity over long run

> 来源：[`intelligenttradingtech.blogspot.com/2010/03/modified-donchian-band-trend-follower.html#0001-01-01`](http://intelligenttradingtech.blogspot.com/2010/03/modified-donchian-band-trend-follower.html#0001-01-01)

这是我在上篇文章中展示的唐奇安通道类型系统的小更新。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjnbXzGoEVYm3Sb-S7ZyjwOFvsFWQrvzskWjoWN88dj8nF1GMap6zryFn4WuTmi1dMLZrSHJ9dPfk3TUCHw1z5Y0LnSZuro-OsWDAasGHsg4ptQ6aHLWC5l1kZImV0WEEw2fxyQ_9yVEN8/s1600/sens_sweepGSPC.jpg)

Fig 1. 参数 n 的净组合买卖增益的敏感性。

使用标普 500 指数作为市场的代理，模拟了指数成立以来的整个生命周期。注意系统在非常短期和更长的周期中都表现出色。短期系统总体表现非常差，并且在任何整体周期（除了可能非常短期）中都没有长期侧的表现好（img/5c13366dd40d90066efc118382a1d599.png）。一个可能的解释是，由于市场向上漂移，短期系统在长期内表现不佳。此外，短期运行没有长期侧的内置复合增长能力，因为它们是不对称的。短期收益的最大值是原始价值的两倍，而长期侧没有限制（克服这一限制的一种方法是使用反向 ETFs）。我相信许多常见的模拟器在计算这种效应和方法上存在错误。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhjQN0MvINmIUKoMnzeEpp4YziXLFAgOVNfIfLSsE54sUHvJvMVbIN4LZ16wSwXdhznJciaB21qK9pokDcmYiECH_9O17Y0eESvjOq3Onrx3lc9wX-xjDJ62MR_Wp-gQpQRU3Aru3hwIIE/s1600/long_term.jpg)

Fig 2. 参数 n=140 的策略的一些长期结果

上述图表显示了在最佳区域附近选择参数的结果。考虑到佣金和短期内策略表现有限，使用策略的长期持仓部分可能会有所回报。另一个观察是，在高度波动的区域可能需要避开，以便捕捉长期策略的有利区域。在早期的帖子中已经提到了一些接近这种政权更迭的方法。

当听到关于“曲线拟合”和优化的批评时，最后一点要考虑的是，正如上述模拟所证明的，你经常会发现局部最优的参数值是最稳健的，因为它在参数化敏感性广泛的范围内表现最佳。
