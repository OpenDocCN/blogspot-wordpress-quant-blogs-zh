<!--yml
category: 未分类
date: 2024-05-18 15:39:57
-->

# Trader Bots | Tr8dr

> 来源：[https://tr8dr.wordpress.com/2009/07/30/trader-bots/#0001-01-01](https://tr8dr.wordpress.com/2009/07/30/trader-bots/#0001-01-01)

July 30, 2009 · 7:23 pm

I came across this [site](http://www.traderbots.com/) today. I’m not a huge believer in technical analysis as a basis for trading, however these guys are doing something interesting. They are generating / seeding strategies as a genetic program based on a combination of technical, momentum, and sentiment inputs into a neural net. These are then bred / cross-pollinated to refine further.

The next part is an extrapolation from the very little they have indicated. I suspect they are doing the following:

1.  Generate initial strategies using a random genetic program that selects inputs from a subset of available technical, sentiment, and momentum indicators.
2.  Calibrate to best possible trading signal (given inputs) using a ANN (neural net)
3.  Evaluate utility function across some years of historical data
4.  Based on results, refine by breeding the strategies with a GA
5.  Rinse and Repeat

It is an automated approach to strategy descovery, avoiding costly manual research. Though it does not appear to make use of more sophisticated inputs & models, the general approach is nice. It would not be a surprise to find that some of these strategies are successful.

The approach can be expanded to incorporate more sophisticated models as inputs (such as basis function based signal decomposition, stochastic state systems, etc).