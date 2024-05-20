<!--yml
category: 未分类
date: 2024-05-12 18:07:21
-->

# A Simple “Follow the Leader” Algorithm | CSSA

> 来源：[https://cssanalytics.wordpress.com/2011/10/12/a-simple-follow-the-leader-algorithm/#0001-01-01](https://cssanalytics.wordpress.com/2011/10/12/a-simple-follow-the-leader-algorithm/#0001-01-01)

A desirable goal of relative strength investing or any type of portfolio algorithm would be to track the best stock/asset from a group of stocks/assets in hindsight. In other words, we wish to use an approach that can “follow the leader.” This goal is a close relative of universal portfolio algorithms (see Universal Portfolios [http://www.stanford.edu/~cover/portfolio-theory.html](http://www.stanford.edu/~cover/portfolio-theory.html)  that seek to track the best pair of  continuously rebalanced stocks/assets in hindsight. Typically a “follow the leader” (FTL) algorithm  is used for online optimization problems in a variety of fields as it has broad applicability and is superior to naaive weighting methodologies. While such algorithms typically use a reward and cost/penalty function to moderate the degree to which the leaders (or successful algorithms) are successful versus unsuccessful, in this post we will take a simplistic approach.

Whether we think of Gold or Apple computer, the key question is how we could have invested most of our money in such stocks by following their trends as they evolved? The answer to this question is that we must seek to track the winners not exclusively on a rolling window basis (like most RS strategies), but rather from the inception or start period of our backtest. Furthermore, we must continuously monitor the leaders and weight our portfolio according to their cumulative return. Finally, to ensure we don’t miss new leaders that start moving during other points in the backtest period, we must repeat this process with multiple start dates. The CSSA SFTL (“S” stands for simple) algorithm works as follows:

1) Inception: track the compound return from the start of the backtest for each asset and each month weight the asset according to their weighted proportion of CAGR with non-negative weights. (asset CAGR / sum of non-zero asset CAGR)

2) Multiple Inception Periods: repeat the same process every 3 months and record a separate set of weights for each inception period

3) Note that you will have a set of asset weights for each inception period that changes every month as the weights change.

4) Use a weighted moving average that weights the oldest periods more than recent periods to ensure that we give more weight to tracking the best asset as recorded since the beginning of the backtest. ie for this month’s period use a weighted average of each of the current weights for all of the recorded inception periods. This is the weight applied to each stock/asset. If one was invariant to the best asset by inception period, you could use a simple moving average that would not favor any one inception period.

This method will invariably track the best asset in hindsight that one could have chosen during the backtest while also providing the opportunity to track the best asset from a variety of inception periods. It is a fairly simple but stable FTL method that could be developed into something more powerful.