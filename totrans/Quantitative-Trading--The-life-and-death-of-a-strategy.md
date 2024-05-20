<!--yml
category: 未分类
date: 2024-05-12 19:01:50
-->

# Quantitative Trading: The life and death of a strategy

> 来源：[http://epchan.blogspot.com/2012/04/life-and-death-of-strategy.html#0001-01-01](http://epchan.blogspot.com/2012/04/life-and-death-of-strategy.html#0001-01-01)

Sometimes it is instructive to look back at some strategies that used to thrive, and then quite suddenly contracted a chronic illness that ultimately led to its demise. It gives us a sense of the unreliability of backtests and curb our over-confidence, which is always useful when dealing with the financial markets.

One good example is a well-known strategy that we called "buy-on-gap". In its simplest version, just buy at the open 100 stocks within the S&P500 which have the lowest returns from their previous day's lows to the current day's open, provided that these returns are lower than one standard deviation. (The standard deviation is computed as the 90-day moving standard deviation of close-to-close returns of a stock.) Exit such  long positions at the day's close.

Many traders know of variants of this strategy, and I started trading it around the beginning of 2007, and in fact, it formed part of my first fund's portfolio of strategies. You can see the cumulative return chart below (click to enlarge) from 2007/01/03-2008/10/29\. The APR is 19%,

*unlevered*

. The Sharpe ratio is 1.4 and the maximum drawdown is just 4%. Note that Lehman Brothers went bankrupt on 2008/09/15, and this is a long-only strategy, yet the performance was spectacular in September-October 2008\. We were patting ourselves furiously on the back.

Now look what happened after this happy period.

 The APR was -6%. 2008/10/29 turned out to be the high watermark.

I have seen some strategies that have the opposite behavior: poor performance prior to 2009, and stellar performance since then. Was there a structural break in the market due to the financial crisis? Was this due to the advent of high frequency trading? The declining volume in the equities market? I will leave these deep questions to financial economists. The only lesson I have learned from this and other examples is that, once a strategy is in decline for some time, it seldom comes back to health, and the best course of action is to bury it swiftly.