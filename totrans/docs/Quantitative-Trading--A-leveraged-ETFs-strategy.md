<!--yml
category: 未分类
date: 2024-05-12 19:00:18
-->

# Quantitative Trading: A leveraged ETFs strategy

> 来源：[http://epchan.blogspot.com/2012/10/a-leveraged-etfs-strategy.html#0001-01-01](http://epchan.blogspot.com/2012/10/a-leveraged-etfs-strategy.html#0001-01-01)

In a

[post](http://epchan.blogspot.ca/2009/07/are-triple-leveraged-etfs-suitable-for.html)

some years ago, I argued that leveraged ETF (especially the triple leveraged ones) are unsuitable for long-term holdings. Today, I want to present research that suggests leveraged ETF can be very

*suitable*

for

*short*

-term trading.

The research in question was just

[published](http://ssrn.com/abstract=2161057)

 by Prof. Pauline Shum and her collaborators at York University. Here is the simplest version of the strategy: if a stock market index has experienced a return >= 2% since the previous day's close up to the current time at 2:15pm ET, then buy this index (via its futures, ETFs, or stock components) right away, and exit at the close with a market-on-close order. Vice versa if the return is <= -2%. The annualized average return from June 2006 to July 2011 was found to be higher than 100%.

Now this strategy is actually quite well-known among institutional traders, although this is the first time I see the backtest results published. The reason why it works is also quite well-known: it has to do with the fact that every leveraged ETF need to rebalance at the market close in order to keep its leverage constant (at x2 or x3, depending on the fund). If the market index goes up, the fund needs to buy the component stocks; otherwise, it needs to sell stocks. If there is major market movement (with absolute return >= 2%) since the previous close, then the amount of stocks that need to be bought or sold will be correspondingly larger, resulting in momentum in all those stocks near the close. This strategy aims to front-run this rebalancing to take advantage of the anticipated momentum.

It has been estimated that if the market moves by 1%, the rebalancing could account for up to 16.8% of the market-on-close volume, so the induced momentum can be substantial. Now who is paying for this profits for those momentum traders? Why, the buy-and-hold investors, of course. This loss for the ETFs shows up as their tracking errors, resulting in a cost of as much as 5% per annum for the buy-and-hold investors. Yet another reason we should not be one of those investors!

As Prof. Shum pointed out, if you trade this strategy live today, you will likely get a lower return, because of all those momentum traders who drove up the price way before the close. However, there may be an ameliorating factor at work here: this momentum is proportional to the NAVof the ETFs. As their NAV goes up with time (either due to additional subscriptions or positive market returns), the returns of this strategy should also increase.

===

Now for some public service announcements:

1) A company called Level 3 Data Corp sells proprietary data indicating buying and selling pressure on stocks. Their internal backtests show that adding these data to some common stock trading strategies essentially double their returns. An explanatory

[video](http://www.youtube.com/watch?v=me1g3PU7nzI)

is available, and I heard they are offering 3-month free trials.

2) The London Systematic Traders (LST) Club has asked me to say a few words about their new initiative to build a London centric collaborative community of traders, developers and researchers.

LST aims to be at the intersection of traders, developers and quants with a strong emphasis community building and on knowledge exchange, providing a trading networks with a very specific focus on systematic, algorithmic (i.e. automated) or quantitative trading.

Membership is free and open to everybody with an interest in the above topics.

[http://www.meetup.com/London-Systematic-Traders/](http://www.meetup.com/London-Systematic-Traders/)

On Friday, Nov 23, I expect to be hosting a Q&A session with members of the LST (see 2 above) at the Apex Hotel in London. All are welcome. Please visit their website for details.

3) I will be conducting my

[Backtesting](http://www.technicalanalyst.co.uk/training/backtestingEC.htm)

and

[Statistical Arbitrage](http://www.technicalanalyst.co.uk/training/statarb.htm)

workshops in London, Nov 19-22, and look forward to seeing some of our readers there!