<!--yml
category: 未分类
date: 2024-05-12 18:56:54
-->

# Quantitative Trading: Time series analysis and data gaps

> 来源：[http://epchan.blogspot.com/2015/07/time-series-analysis-and-data-gaps.html#0001-01-01](http://epchan.blogspot.com/2015/07/time-series-analysis-and-data-gaps.html#0001-01-01)

Most time series techniques such as the ADF test for stationarity, Johansen test for cointegration, or ARIMA model for returns prediction, assume that our data points are collected at regular intervals. In traders' parlance, it assumes bar data with fixed bar length. It is easy to see that this mundane requirement immediately presents a problem even if we were just to analyze daily bars: how are we do deal with weekends and holidays?

You can see that the statistics of return bars over weekdays can differ significantly from those over weekends and holidays. Here is a table of comparison for SPY daily returns from 2005/05/04-2015/04/09:

|  |  |  | **Mean Absolute Returns (bps)** |  |
|  |  |  |  |  |
|  |  |  |  |  |

Though the absolute magnitude of the returns over a weekday is similar to that over a weekend, the mean returns are much more positive on the weekdays. Note also that the kurtosis of returns is almost doubled on the weekends. (Much higher tail risks on weekends with much less expected returns: why would anyone hold a position over weekends?) So if we run any sort of time series analysis on daily data, we are force-fitting a model on data with heterogeneous statistics that won't work well.

The problem is, of course, much worse if we attempt time series analysis on intraday bars. Not only are we faced with the weekend gap, in the case of stocks or ETFs we are faced with the overnight gap as well. Here is a table of comparison for AUDCAD 15-min returns vs weekend returns from 2009/01/01-2015/06/16:

|  |  |  | **Mean Absolute Returns (bps)** |  |
|  |  |  |  |  |
|  |  |  |  |  |

In this case, every important statistic is different (and it is noteworthy that kurtosis is actually lower on the weekends here, illustrating the mean-reverting character of this time series.)

So how should we predict intraday returns with data that has weekend gaps? (The same solution should apply to overnight gaps for stocks, and so omitted in the following discussion.) Let's consider several proposals:

1) Just delete the weekend returns, or set them as NaN in Matlab, or missing values NA in R. 

This won't work because the first few bars of a week isn't properly predicted by the last few bars of the previous week. We shouldn't use any linear model built with daily or intraday data to predict the returns of the first few bars of a week, whether or not that model contains data with weekend gaps. As for how many bars constitute the "first few bars", it depends on the lookback of the model. (Notice I emphasize linear model here because some nonlinear models can deal with large jumps during the weekends appropriately.)

2) Just pretend the weekend returns are no different from the daily or intraday returns when building/training the time series model, but do not use the model for predicting weekend returns. I.e. do not hold positions over the weekends.

This has been the default, and perhaps simplest (naive?) way of handling this issue for many traders, and it isn't too bad. The predictions for the first few bars in a week will again be suspect, as in 1), so one may want to refrain from trading then. The model built this way isn't the best possible one, but then we don't have to be purists.

3) Use only the most recent period without a gap to train the model. So for an intraday FX model, we would be using the bars in the previous week, *sans* the weekends, to train the model. Do not use the model for predicting weekend returns nor the first few bars of a week.

This sounds fine, except that there is usually not enough data in just a week to build a robust model, and the resulting model typically suffers from severe data snooping bias.

You might think that it should be possible to concatenate data from multiple gapless periods to form a larger training set. This "concatenation" does not mean just piecing together multiple weeks' time series into one long time series - that would be equivalent to 2) and wrong. Concatenation just means that we maximize the total log likelihood of a model over multiple independent time series, which in theory can be done without much fuss since log likelihood (i.e. log probability) of independent data are additive. But in practice, most pre-packaged time series model programs do not have this facility. (Do add a comment if anyone knows of such a package in Matlab, R, or Python!) Instead of modifying the guts of a likelihood-maximization routine of a time series fitting package, we will examine a short cut in the next proposal.

4) Rather than using a pre-packaged time series model with maximum likelihood estimation, just use an equivalent multiple linear regression (LR) model. Then just fit the training data with this LR model with all the data in the training set except the weekend bars, and use it for predicting all future bars except the weekend bars and the first few bars of a week.

This conversion of a time series model into a LR model is fairly easy for an autoregressive model AR(p), but may not be possible for an autoregressive moving average model ARMA(p, q). This is because the latter involves a moving average of the residuals, creating a dependency which I don't know how to incorporate into a LR. But I have found that AR(p) model, due to its simplicity, often works better out-of-sample than ARMA models anyway. It is of course, very easy to just omit certain data points from a LR fit, as each data point is presumed independent. 

Here is a plot of the out-of-sample cumulative returns of one such AR model built for predicting 15-minute returns of NOKSEK, assuming midpoint executions and no transaction costs (click to enlarge.)

Whether or not one decides to use this or the other techniques for handling data gaps, it is always a good idea to pay some attention to whether a model will work over these special bars.

===

This is a new online workshop focusing on the practical use of AI techniques for identifying predictive indicators for asset returns.

===

**Managed Accounts Update**

Our FX Managed Account program is 6.02% in June (YTD: 31.33%).

===

**Industry Update**

*   I previously [reported](http://epchan.blogspot.com/2014/02/fundamental-factors-revisited-with.html) on a fundamental stock model proposed by Lyle and Wang using a linear combination of just two firm fundamentals ― book-to-market ratio and return on equity. Professor Lyle has [posted](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=2613366) a new version of this model.

*   Charles-Albert Lehalle, Jean-Philippe Bouchaud, and Paul Besson reported that "intraday price is more aligned to signed limit orders (cumulative order replenishment) rather than signed market orders (cumulative order imbalance), even if order imbalance is able to forecast short term price movements." Hat tip: [Mattia Manzoni](https://it.linkedin.com/pub/mattia-manzoni/45/670/b01/en). (I don't have a link to the original paper: please ask Mattia for that!)

*   A new investment competition to help you raise capital is available at [hedgefol.io](http://hedgefol.io/).

*   Enjoy an **Outdoor Summer Party** with fellow quants benefiting the New York Firefighters Burn Center Foundation on Tuesday, July 14th with great food and cool drinks on a terrace overlooking Manhattan. Please [RSVP](http://quantsgiveback.org/event/) to join quant fund managers, systematic traders, algorithmic traders, quants and high frequency sharks for a great evening. This is a **complimentary** event (donations are welcomed). 

**===**

Follow me on Twitter: @chanep