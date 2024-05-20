<!--yml
category: 未分类
date: 2024-05-18 14:05:26
-->

# The Importance of Return Distributions – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2010/05/04/the-importance-of-return-distributions/#0001-01-01](https://quantumfinancier.wordpress.com/2010/05/04/the-importance-of-return-distributions/#0001-01-01)

When designing a strategy, I like to observe the probability distribution of the asset I plan to trade. It yields precious information on the behavior of the underlying and can also help identify the market regime in effect for a given period.

Of course eyeballing the probability density curve or the empirical cumulative distribution can work, but from a quantitative trading point of view, it does not really help; we want something more mechanical that we can rely on over and over. The answer is quite simple; simple curve analysis can give us the mechanical capability we are looking for. Data on the mean, median, skew, kurtosis, etc. of a distribution can all be fed as parameters to be analyzed in a trading system.

We don’t have to use this technique uniquely on raw return data, it is often helpful to know how a given indicator or strategy affect the return distribution. A comparison between the raw return distribution and one processed with signals from a strategy can help indicate whether the strategy is traded with the right bias for the current market regime or if a strategy is suddenly diminishing in profitability. Furthermore, for the daily swing traders amongst us, probability densities analysis can help us see if our indicators really help mitigate daily MR.

Finally, distribution analysis can be an extremely valuable tool when developing adaptive strategies. It provides a strategy with instant feedback on its performance and its effect on the return series of the underlying; taking that in consideration can be a good base to build on when designing your own adaptive algorithms (more on that later..).

QF