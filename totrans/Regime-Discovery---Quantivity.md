<!--yml
category: 未分类
date: 2024-05-18 13:53:39
-->

# Regime Discovery | Quantivity

> 来源：[https://quantivity.wordpress.com/2010/02/15/regime-discovery/#0001-01-01](https://quantivity.wordpress.com/2010/02/15/regime-discovery/#0001-01-01)

When considering [market regime](https://quantivity.wordpress.com/2009/12/31/market-regime-trading-redux/), many traders think first of macro principles: business cycle, risk appetite, interest rates, liquidity, market volatility, *etc*. This perspective is motivated by applying [herd behavior](http://en.wikipedia.org/wiki/Herd_behavior) to market dynamics: regimes arise when many people either trade in harmony (trends) or disharmony (range). In this sense, herd behavior is an [unobservable](https://quantivity.wordpress.com/2010/02/15/trading-the-unobservable/) for regimes.

Yet, this explanation is not terribly insightful for trading: either one must predict the future or settle for exploiting established trends (*i.e.* macroeconomic forecasting or trend following). Although both strategies are actively traded, profits tend to be unpredictable.

An alternative approach is trying to build *regime discovery* models which quantitatively identify regimes early in their formation, and probabilistically inform how to trade ahead of the herd (whether by seconds or days). For example, how price or volatility of HP, VGT, and DJIA change in relation to a price change in IBM. Alternatively, how USD crosses change in response to an unobserved Fed intervention.

How to formulate this type of discovery model is not obvious. What follows is a sketch, which readers are encouraged to comment upon.

Begin by positing:

> Regime discovery drives prices and volatility via [second-order causal](https://quantivity.wordpress.com/2010/01/10/causality-exogeny-regimes/) information diffusion.

In other words: a price change in one security will cause one or more other securities to correspondingly change price. Alternatively, by analogy; think of a pebble thrown in a lake:

*   Lake: the universe of *observable variables*, consisting of all time-series observable from worldwide exchanges and OTC (although not accessible to retail traders, this universe is available to quant HFs with good connectivity)
*   Pebble: event which causes a price change for a *single* instrument at a *single* point in time

Framed this way, regime discovery requires a model for how prices across multiple instruments sequentially change over time in response to a price change of a single instrument (*i.e.* an inter-instrument sequential price model). Thus, a corresponding model should be potentially applicability to any market which trades multiple securities whose prices are empirically believed to be driven by information diffusion:

*   Equities: price change in one instrument resulting in price/vol changes in others due to ETF composition, pairs trading, hedging, *etc*.
*   FX: central bank intervention resulting in updated quotes/trades being propagated across dealers
*   IR: changes in central bank rates resulting in price/vol changes across credit and equity instruments

Models for expressing inter-instrument sequential price/vol changes warrant research. [Tr8dr](http://tr8dr.wordpress.com/) recently authored several interesting posts applying clustering and correlation, including [minimum spanning trees for inter-asset correlations](http://tr8dr.wordpress.com/2009/12/28/10-years/) and [equity clusters](http://tr8dr.wordpress.com/2009/12/30/equity-clusters/). Older literature includes interesting articles by [Zoran Obradovic](http://www.ist.temple.edu/%7Ezoran/) (mid-1990s), [Takayuki Mizuno](http://en.scientificcommons.org/takayuki_mizuno), and [Laszlo Gillemot](http://en.scientificcommons.org/laszlo_gillemot).