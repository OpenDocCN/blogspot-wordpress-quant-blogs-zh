<!--yml
category: 未分类
date: 2024-05-18 04:44:01
-->

# Intelligent Trading: IBS reversion edge with QuantShare

> 来源：[http://intelligenttradingtech.blogspot.com/2013/01/ibs-reversion-edge-with-quantshare.html#0001-01-01](http://intelligenttradingtech.blogspot.com/2013/01/ibs-reversion-edge-with-quantshare.html#0001-01-01)

Happy New Years to readers; my resolution this year is to continue delivering thoughts and ideas to others in the hopes that we all might be able to benefit somewhat from sharing observations. I'll start by describing an edge using

[QuantShare](http://www.quantshare.com/)

as the back-testing engine.

                                Fig 1\. Optimized (overfit) SPY IBS Long run Performance

Have you ever had an edge that worked fairly well and then suddenly found that it was almost simultaneously revealed across several sources? This seemed to be the case with an edge I had discovered some time back via data mining. I first noticed it was divulged in a recent copy of Active Trader, '

[The low-close edge](http://www.activetradermag.com/index.php/c/Trading_Strategies/d/The_low-close_edge)

,' by Nat Stewart. Later, I found the concept had also spread out into the blogosphere. Two notable write-ups can be found

[here](http://adaptivetrader.wordpress.com/2012/12/28/cumulative-ibs-indicator/)

and

[here](http://qusma.com/2012/11/06/closing-price-in-relation-to-the-days-range-and-equity-index-mean-reversion/)

.  The acronym IBS seems to be the buzzword floating around, so I'll continue to use it here. IBS stands for Internal Bar Strength (not to be confused with the IBS that many traders might have developed over the years). The strength indicator is described with an extremely simple equation:

$IBS = \dfrac{Close - Low}{High -Low}$

What it describes is the relative position of the close with respect to the low to high range of the period. When Jaffray Woodriff was interviewed in the latest Hedge Funds Wizards book, he described a very simple predictive indicator (based only upon transformations of the Open, High, Low, and Close of the data) that had proved remarkably stable over the years. It inspired some

[debate](http://stats.stackexchange.com/questions/31513/new-revolutionary-way-of-data-mining)

in statistical and machine learning circles, but nevertheless, sparks images of a holy grail. If there was ever a hypothesis model that came close to his description, I'd certainly consider this as a candidate for the reversion side. In addition to simplicity, one of the reasons it is so useful is that unlike many other approaches at feature transformation of raw financial series, it is scale invariant and does not require any further scaling to support non-stationary data. The results of the transformation will always be bound between 0 and 100%. So the transformed features will always be bound inside of a fixed and finite space regardless of the evolving data properties (a great property for machine learning). The algorithm runs very fast and does not require frequent readjusting of model parameters unlike many online or econometric based models.

The system simply buys at the close when the IBS indicator closes near the low end of the day and goes short when the indicator closes near the high of the day; exit is next day close.  Much of the time the indicator is neutral or no trade, allowing a good net risk adjusted return with low exposure. The thresholds, while often mentioned as being set to the 0.25 and 0.75 quartiles of the range, can be adjusted or found manually in the optimization settings.

                               Fig 2\. Performance fit In Sample Optimization (to 2000).

In order to avoid hindsight bias and over-fitting error (as in Fig 1.), I show an optimization using only in sample data for SPY (yahoo data) up to the year 2000 (rank sorted by CAGR and Sharpe). One interesting thing we notice is that the higher threshold is actually optimized to 1, meaning no reversion from the high/short side. This is consistent with what we would expect with a long bias/drift market. We always have to be careful about systematic shorting with a market that has long term positive drift. 

                                 Fig 3\. In Sample/ Out of Sample Performance

                                           with In Sample fitted parameters.

Fortunately, even without the short high reversion side, the system performed well for the rest of the out of sample data (Fig 3.).   A last comment is that looking at the over-fit data should gives us some insight about reversion systems and high volatility sell off regimes.

I've attached code to allow readers to repeat results.

Simulated back-test results long only. $10,000 Principle. No Slippage/Comm. incl.