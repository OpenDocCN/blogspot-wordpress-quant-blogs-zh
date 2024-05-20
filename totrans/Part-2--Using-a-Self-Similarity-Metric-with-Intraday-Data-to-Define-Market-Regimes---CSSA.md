<!--yml
category: 未分类
date: 2024-05-12 17:47:31
-->

# Part 2: Using a Self-Similarity Metric with Intraday Data to Define Market Regimes | CSSA

> 来源：[https://cssanalytics.wordpress.com/2015/04/17/part-2-using-a-self-similarity-metric-with-intraday-data-to-define-market-regimes/#0001-01-01](https://cssanalytics.wordpress.com/2015/04/17/part-2-using-a-self-similarity-metric-with-intraday-data-to-define-market-regimes/#0001-01-01)

The Self-Similarity metric has been a popular series. Recently the [original post](https://cssanalytics.wordpress.com/2015/03/13/using-a-self-similarity-metric-with-intraday-data-to-define-market-regimes/ "Using a Self-Similarity Metric with Intraday Data to Define Market Regimes") was shared on Jeff Swanson’s popular site [System Trader Success](http://systemtradersuccess.com/) which covers a wide variety of thought provoking articles on trading system development and is worth reading. Jeff has also posted some TradeStation code for the indicator which some readers may find valuable. In a great example of vertical blogging, a very interesting analysis on the Self-similarity metric was done by Mike Harris on his [Price Action Blog](http://www.priceactionlab.com/Blog/2015/04/performance-in-stable-and-chaotic-markets-based-on-the-cssa-regime-indicator/) which also has a lot of very interesting articles and is worth following.

I have to say that one of the most rewarding aspects of this blog has been my interaction with readers (and fellow bloggers) at various levels. I have developed several relationships over the years, and some of these developed into new business opportunities. Many years ago while actively running CSS Analytics, I was fortunate to work with a core group of very talented and dedicated people. It has been nice to see that many of these individuals have become quite successful in the quant world. One of the original members of that talented group was David Abrams. We have spent a lot of time on system development over the years, and although we no longer actively collaborate we still manage to keep in touch. David reached out to me with some visuals and analysis on the chaos/stability self-similarity indicator I recently presented on the blog. I suggested that we post this for CSSA readers, and he was kind enough to agree to share.

**Dave Abrams is Director of Quantitative Strategies at Wilbanks, Smith and Thomas Asset Management (www.wstam.com) in Norfolk, VA, where they design risk managed fund models and S&P indices (about 400M of the firm’s 2.5B in AUM is quant). He was formerly part of a group doing quant research at CSS Analytics.**

**Visualizing The Chaos Stability Indicator**

It is useful to visualize DV’s new self-similarity regime method in a Tradestation chart. Here is the strategy and indicator using the default parameters (N = 10 day, 60 day average, 252 percent rank length). I transformed the indicator by subtracting 0.5 to center the values around 0 and displayed with a color coded histogram.

Here is what the Chaos Stability as a buy/sell indicator on the SPY looks like:

[![pic 1](img/cf7f670bd594ab44935022f85f0f6f74.png)](https://cssanalytics.files.wordpress.com/2015/04/pic-1.png)

The indicator is currently in a new “sell” position as the value is below zero.
This perhaps reflects the more random and sideways market movement that we have had over the past few months. As with any indicator, this bearish signal is not perfect and in April through early July of 2014 the market made good upward progress despite the chaos stability values being mired deep in the red. It is useful to look at some other charts to get a sense of when the buy and sell signals occur.

[![pic2](img/032da0d5761afc85201091efc2527583.png)](https://cssanalytics.files.wordpress.com/2015/04/pic2.png)

[![pic3](img/665c954dbd9f7b0e1d7fe034e1c11cf8.png)](https://cssanalytics.files.wordpress.com/2015/04/pic3.png)

[![pic 1](img/cf7f670bd594ab44935022f85f0f6f74.png)](https://cssanalytics.files.wordpress.com/2015/04/pic-1.png)

[![pic4](img/964f894b3eae491868cf2c080acf6e71.png)](https://cssanalytics.files.wordpress.com/2015/04/pic4.png)

It is hard to discern what is going on without careful inspection, but it seems as if the chaos/stability indicator flashes buy signals at swing lows- where the market is moving persistently downward or in persistent bull moves upward out of corrections or at the top of established rallies. Sell signals tend to occur near market tops where things get choppy or in areas of congestion where the market is moving sideways within its long-term trend. Since persistency occurs both in up and down moves, signals are uncorrelated or even negatively correlated to a trend-following strategy as highlighted in the original post. This is important to those looking to diversify a trend strategy on a single asset.

**Smoothed Chaos Stability Metric**

One of the challenges I noticed when looking at the charts was that the indicator frequently switched from buy to sell- especially as the value hovered close to zero. Smoothing seemed to be a logical approach to reduce some of the whipsaw trades and reduce turnover. To address this issue, I applied John Ehler’s Super Smoother method ([http://traders.com/Documentation/FEEDbk_docs/2014/01/TradersTips.html](http://traders.com/Documentation/FEEDbk_docs/2014/01/TradersTips.html)) to to the Chaos Stability measure. Notice the indicator below. This reduced the number of trades by 11% and the Profit Factor went up by 6 %.

[![pic5](img/b68ac309fc9e5c9109547efddfaddeff.png)](https://cssanalytics.files.wordpress.com/2015/04/pic5.png)

**Walk Forward Analysis**

One of the challenges of new indicators is that they tend to promise a lot but fail to deliver in the real world. Often the reason this happens is because the examples presented by the developer are tuned to a specific set of parameters- in other words the indicator is over fit and is not robust. So is DV’s innovative new indicator just lucky or is it stable? One of the best ways to evaluate whether an indicator has any predictive power is to perform a walk forward test. An indicator with no predictive power will tend to fail using such tests. For this evaluation, I did a walk-forward test in Tradestation. This module continuously re-optimizes the parameters so that at each period of time we are using out-of-sample results. We can get greater confidence in the strategy if it performs well using walk-forward. The results are below :

[![pic 6](img/15edd3a2855506ca85823fb70ac1c8f4.png)](https://cssanalytics.files.wordpress.com/2015/04/pic-6.png)

Based on these criteria for evaluation, the DV Chaos/Stability indicator passes with flying colors. In addition to passing the walk-forward test the logic of indicator is also sound- which is an often overlooked but important qualitative assessment. In our quantitative research methodology we always apply a walk-forward analysis and qualitative assessment. The hypothetical equity curve from the walk-forward results showing each out-of-sample period over time are presented below.

[![pic7](img/f21d683b82c99565c5ddf8291e281b51.png)](https://cssanalytics.files.wordpress.com/2015/04/pic7.png)

Tradestation Walk Forward Analyzer Performance Graph. The results are hypothetical results and are NOT an indicator of future results and do NOT represent returns that any investor actually attained

Good quantitative research is a combination of different but stable ideas which either confirms each other or adds diversity to the overall model. I agree with Ray Dalio that 15 uncorrelated return streams is the holy grail of investing (
[http://www.businessinsider.com/heres-the-most-genius-thing-ray-dalio-said-2011-9](http://www.businessinsider.com/heres-the-most-genius-thing-ray-dalio-said-2011-9)). DV’s chaos stability regime model could be a viable uncorrelated candidate.

Disclosure

The research discussion presented above is intended for discussion purposes only and is not intended as investment advice, recommendation of any particular investment strategy including any of the depicted models. There are inherent limitations of showing portfolio performance based on hypothetical & back-tested results. Unlike an actual record, hypothetical results cannot accurately reflect the effect of material economic or market factors on the price of the securities, and therefore, results may be over or under-stated due to the impact of these factors. Since hypothetical results do not represent actual trading and may not accurately reflect the impact of material economic and market factors, it is unknown what effect these factors might have had on the model depicted above. Past performance, whether based on hypothetical models or actual investment results, is not indicative of future performance.