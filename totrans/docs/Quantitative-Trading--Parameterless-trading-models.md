<!--yml
category: 未分类
date: 2024-05-12 19:20:24
-->

# Quantitative Trading: Parameterless trading models

> 来源：[http://epchan.blogspot.com/2008/05/parameterless-trading-models.html#0001-01-01](http://epchan.blogspot.com/2008/05/parameterless-trading-models.html#0001-01-01)

A portfolio manager that I used to work for like to pronounce that his trading models have "no free parameters". As is customary in our secretive industry, he would not elaborate further on his technique.

Lately, I begin to understand what a trading model with no free parameter means. It doesn't mean that it does not contain any lookback period for calculating trends, or thresholds for entry or exit. I think that would be impossible. It just means that all such parameters are

dynamically

optimized in a moving lookback window. This way, if you ask: "Does the model have a fixed profit cap?", the trader can honestly reply: "No, profit cap is not an input parameter. It is determined by the model itself."

The advantage of a parameterless trading model is that it minimizes the danger of overfitting the model to multiple input parameters. (The so-called "data-snooping bias".) So the backtest performance should be much closer to the actual forward performance.

Now, it is quite computationally challenging to optimize all these parameters just-in-time for your next order, but it is often even more difficult to do that in a backtest, given that a multidimensional optimization need to be performed for each historical bar. As a result, I personally have seldom traded parameterless models, until I get to research my

[regime-switching model](http://epchan.blogspot.com/2008/05/machine-learning-regime-switching.html)

. That model is almost parameterless (I left out a few parameters from optimization because of a lack of time, not because of any technical difficulties).

The reason backtest optimization can now be done within a few minutes is due to my use of Alphacet Discovery's server-based optimization engine. There may be other optimization software out there that performs similar functions efficiently -- I welcome comments from the reader.