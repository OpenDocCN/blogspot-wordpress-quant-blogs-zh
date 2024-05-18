<!--yml
category: 未分类
date: 2024-05-18 13:55:59
-->

# Levered ETFs and Market Close | Quantivity

> 来源：[https://quantivity.wordpress.com/2009/07/28/leveraged-etfs-market-close/#0001-01-01](https://quantivity.wordpress.com/2009/07/28/leveraged-etfs-market-close/#0001-01-01)

Cheng and Madhavan from [BGI](http://www.barclaysglobal.com/) recently published a research article entitled [“The Dynamics of Leveraged and Inverse Exchange-Traded Funds”](http://www.barclaysglobal.com/secure/repository/publications/usa/ResearchPapers/Leveraged_ETF.pdf). This article models and analyzes numerous dynamics of levered ETF, for which traders may be unaware: daily returns, return divergence, path dependency, tracking errors vs underlying, rebalancing, and hedging.

Their results motivate a seemingly-contradictory (and *a priori* unexpected) hypothesis: *side effects of levered ETF will influence behavior of quantitative strategies which do not trade the corresponding ETFs*. To use a [quantum mechanics](http://en.wikipedia.org/wiki/Quantum_mechanics) analogy: levered ETFs will have [action at a distance](http://en.wikipedia.org/wiki/Action_at_a_distance_(physics)) effect on wholly-unrelated strategies.

This absurd-sounding relationship is driven by hedging and closing prices, as extant funds promise a multiple of the underlying *daily* return. The following quote from the article sums up the hedging argument (p. 9):

> Hedging demand provides an additional momentum effect to same-day returns that increases the price pressure effect of any signed order inbalance regardless of its source…The presence of the hedge induces serial correlation in returns because the previous period’s hedge is linearly related to the previous return. Thus, hedging flows in leveraged and inverse ETFs can exacerbate same-day volatility, add momentum effects, and induce serial correlation in returns.

In other words, momentum and serial correlation of underlying returns will be magnified by leveraged ETF hedging. While readers may be inclined to dismiss this effect as inconsequential, the impact is unexpectedly *massive* (p. 11 and Table 5):

> A broad 1% move in the US equity market would result in additional MOC demand of about 17%, while a 5% move is associated with demands equal to 50% of the close.

Wow! This effect is not surprising in retrospect, as it is driven by simple arithmetic:

> Since we are essentially computing a weighted average, the market-on-close demand in value terms is just a linear function of return. However, the demand as a fraction of closing volume is a non-linear function of return because the re-balancing demand is added to the denominator too.

Further, “as [AUM](http://en.wikipedia.org/wiki/Assets_under_management) changes and more levered and ultra short products gain traction, we would expect this slope to steepen” (p. 11). In other words, this effect will only become more dominant as these ETFs gain further traction.

At this point, readers may well be asking what any of this has to do with *unrelated* strategies. The crux is closing prices: many strategies depend upon closing prices, whether directly or indirect. Examples range from the well-documented overnight effect (*e.g.* [Goldman](http://www.bloomberg.com/apps/news?pid=newsarchive&sid=aXhs9g9il2rk)) to the myriad close-to-close strategies. In this vein, authors calculate numerous regressions based upon rebalancing flows. The effects are equally interesting:

> Closing period is 15.4% of the total trading day, but is a higher fraction (about 25%) of the day’s volume and hence of the day’s return as implied by the estimates. The estimate of β [2] suggests that after controlling for the day’s return movement, $1 billion of re-balancing flow adds 0.54% to the closing period’s return

Finally, using the daily value of [VIX](http://finance.yahoo.com/q?s=%5EVIX), the authors evaluate the relationship between rebalancing flows and closing period volatility. Predictably, the result is “greater imbalances add to closing volatility” (p. 13).

For those readers running close-to-close strategies, this may partially contribute to the increasing instabilities observed over the past few months. Finally, rebalancing and hedging flows beg for strategies to exploit “predictable and concentrated trading activity near the market closes” (p. 22).