<!--yml
category: 未分类
date: 2024-05-12 20:29:31
-->

# Falkenblog: Minimum Volatility Portfolio Tactics

> 来源：[http://falkenblog.blogspot.com/2012/05/minimum-volatility-portfolio-tactics.html#0001-01-01](http://falkenblog.blogspot.com/2012/05/minimum-volatility-portfolio-tactics.html#0001-01-01)

MSCI is very good at creating indices, and their

[Global Minimum Volatility Index](http://www.msci.com/products/indices/strategy/risk_premia/minimum_volatility/)

is intriguing (BB ticker M00IWO$P). If I plot its return again a simple average of

[my Minimum Variance portfolios](http://www.betaarbitrage.com/)

drawn from the UKX, NKY, MSER and SPX indices (UK, Japan, Europe, USA). They line up pretty well.  Mean returns and standard deviations are basically identical over the period for which I have MSCI Global Minimum volatility data.

My index is created by taking all the constituents of these major indices each 6 months and applying an optimization algorithm that minimizes variance using the prior year's daily data.  The solution defines a fixed set of weights over the next 6 months.  MSCI weights things more globally, and has 8 different constraints.  It seems if you simply want a worldwide minimum variance, the little constraints about industries etc don't matter much in  risk/return effect.  This highlights that this problem has a 'flat maximum' in that solutions that are not so close to each other on one level are really close in terms of the ultimate answer.  See Robin Dawes'

[The Robust Beauty of Improper Linear Models](http://heatherlench.com/wp-content/uploads/2008/07/dawes2.pdf)

for more on this phenomenon (strangely, the first page of Google search results for this title was

[a music CD released in 1995](http://www.discogs.com/Chris-Stamey-and-Kirk-Ross-The-Robust-Beauty-Of-Improper-Linear-Models-In-Decision-Making/release/401743)

.  I guess these artists are being ironic).

The real value-add to any low vol strategy is not their low volatility algorithm, but rather, strategic decisions about how to view complementary factors like idiosyncratic volatility, size, momentum, and value.  Everything here is correlated, and so implicitly ignoring these factors is impossible. The details that will matter are really based on assumptions on how these factors interact: whether factor returns cancel each other  out or add up, and this answer varies whether you look at these factors like

[characteristics as opposed to a latent risk factors](http://seekingalpha.com/article/309986-identifying-portfolio-risk-characteristics-vs-factors)

.