<!--yml
category: 未分类
date: 2024-05-12 18:56:20
-->

# Quantitative Trading: Really, Beware of Low Frequency Data

> 来源：[http://epchan.blogspot.com/2016/09/really-beware-of-low-frequency-data.html#0001-01-01](http://epchan.blogspot.com/2016/09/really-beware-of-low-frequency-data.html#0001-01-01)

I wrote in a

[previous article](http://epchan.blogspot.com/2015/04/beware-of-low-frequency-data.html)

 about why we should backtest even end-of-day (daily) strategies with intraday quote data. Otherwise, the performance of such strategies can be inflated. Here is another brilliant example that I came across recently.

Consider the oil futures ETF USO and its evil twin, the inverse oil futures ETF DNO*. In theory, if USO has a

*daily*

return of x%, DNO will have a daily return of -x%. In practice, if we plot the daily returns of DNO against that of USO from 2010/9/27-2016/9/9, using the usual consolidated end-of-day data that you can find on Yahoo! Finance or any other vendor,

we see that though the slope is indeed -1 (to within a standard error of 0.004), there are many days with significant deviation from the straight line. The trader in us will immediately think "arbitrage opportunities!"

Indeed, if we backtest a simple mean reversion strategy on this pair - just buy equal dollar amount of USO and DNO when the sum of their daily returns is less than 40 bps at the market close, hold one day, and vice versa - we will find a strategy with a decent Sharpe ratio of 1 even after deducting 5 bps per side as transaction costs. Here is the equity curve:

Looks reasonable, doesn't it? However, if we backtest this strategy again with BBO data at the market close, taking care to subtract half the bid-ask spread as transaction cost, we find this equity curve:

We can see that the problem is not only that we lose money on practically every trade, but that there was seldom any trade triggered. When the daily EOD data suggests a trade should be triggered, the 1-min bar BBO data tells us that in fact there was no deviation from the mean.

(By the way, the returns above were calculated before we even deduct the borrow costs of occasionally shorting these ETFs. The "rebate rate" for USO is about 1% per annum on Interactive Brokers, but a steep 5.6% for DNO.)

In case you think this problem is peculiar to USO vs DNO, you can try TBT vs UBT as well.

Incidentally, we have just verified a golden rule of financial markets: apparent deviation from efficient market is allowed when no one can profitably trade on the arbitrage opportunity.

===

*Note: according to www.etf.com, "The issuer [of DNO] has temporarily suspended creations for this fund as of Mar 22, 2016 pending the filing of new paperwork with the SEC. This action could create unusual or excessive premiums— an increase of the market price of the fund relative to its fair value. Redemptions are not affected. Trade with care; check iNAV vs. price." For an explanation of "creation" of ETF units, see my article "

[Things You Don't Want to Know about ETFs and ETNs](http://epchan.blogspot.ca/2016/06/some-things-you-dont-want-to-know-about.html)

".

===

**Industry Update**

*   Quantiacs.com just recently registered as a CTA and operates a marketplace for trading algorithms that anyone can contribute. They also published an educational blog post for Python and Matlab backtesters: https://quantiacs.com/Blog/Intro-to-Algorithmic-Trading-with-Heikin-Ashi.aspx

*   I will be moderating a panel discussion on "How can funds leverage non-traditional data sources to drive investment returns?" at [Quant World Canada](http://www.terrapinn.com/conference/quant-world-canada/) in Toronto, November 10, 2016. 

===

**Upcoming Workshops**

Momentum strategies are for those who want to

*benefit*

from tail events. I will discuss the fundamental reasons for the existence of momentum in various markets, as well as specific momentum strategies that hold positions from hours to days.

A senior director at a major bank wrote me: "…thank you again for the Momentum Strategies training course this week. It was very beneficial. I found your explanations of the concepts very clear and the examples well developed. I like the rigorous approach that you take to strategy evaluation.”