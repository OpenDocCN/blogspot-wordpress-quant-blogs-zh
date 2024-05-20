<!--yml
category: 未分类
date: 2024-05-12 19:00:22
-->

# Quantitative Trading: Order flow as a predictor of return

> 来源：[http://epchan.blogspot.com/2012/10/order-flow-as-predictor-of-return.html#0001-01-01](http://epchan.blogspot.com/2012/10/order-flow-as-predictor-of-return.html#0001-01-01)

Order flow is signed transaction volume: if an order is executed at the ask price, the incremental order flow is +(order size); if executed at the bid price, it is -(order size). In certain markets where traders can only buy and sell from market makers but not from each other, a positive order flow means that traders are net buyers of a security. But even in markets where everyone can place and fill orders on a common order book, a positive order flow indicates that informed traders (those willing to aggressively get into a position) are eagerly acquiring a security.

The neat thing about order flow is that it has proven to be a good momentum indicator. That is to say, a positive flow predicts a positive future return. This might seem trivially obvious, but you have remember that generally speaking, a positive past return by no means predicts a positive future return. That FX order flow possesses this predictive power was shown by Evans and Lyons in a series of

[papers](http://www.bis.org/publ/bppdf/bispap02j.pdf)

, but this indicator is useful in many other markets, and at many different time scales. For example, in a

[paper](http://www.people.hbs.edu/estafford/Papers/AFS.pdf)

by Coval and Stafford, it was shown that if you can tease out the order flow of a stock due to mutual funds' trading alone, you can also predict its future return up to, say, a quarter. This paper not only shows that order flow is predictive, but that sometimes a specific kind of order flow (in this case, that of mutual funds only) is sometimes more predictive than general order flow. In many cases, traders find that by counting only order flow due to institutional traders, or order flow due to large orders, they can better predict future returns. (No wonder institutional traders are trying their darnedest to break up their orders into small chunks, or to trade in dark pools!) I recently also heard that order flow into sector ETFs can be predictive of that sector's return. If any reader has read papers or has experience with this type of sector rotation model, please leave a comment!

Despite the proven usefulness of order flow, not too many retail traders utilize it. The reason is simple: it can be hard to measure. In FX in particular, many markets do not report trade information, or they report with a sufficient delay such that the information has no predictive utility. Even for markets that report instantaneous trade information, you would need a good piece of software to capture every bid, ask, trade, and trade size, and store them in an array, in order to compute order flow, an operation that most retail trading software cannot accomplish. However, this barrier to entry may just mean that there are still decent alpha to be extracted from this indicator.

Now, a bunch of public service announcements ...

===

A new algorithmic trading platform called Rizm designed for retail traders is now available. You can sign up for their beta trial

[here](http://equametrics.com/)

.

===

[Quantopian](https://app.quantopian.com/posts/ernie-chans-gold-vs-gold-miners-stat-arb)

has created an event-driven version of my

[gold/gold-miners arb strategy](http://epchan.blogspot.ca/2011/06/when-cointegration-of-pair-breaks-down.html)

 with source codes and analysis available. I find that the performance metrics clear and useful: better than the output from my own backtest programs! (Quantopian is a platform where you can share backtest results and codes with other traders.)

===

[Arbmaker](http://arb-maker.com/)

 is a platform for pair traders, and it incorporates software for cointegration tests, has integrated data feed from many vendors, and allows automated order submission to Interactive Brokers. Neural networks and Kalman filter are also included.

===

Finally, I will be giving a talk titled "Backtesting and Its Pitfalls" at the World MoneyShow at the Metro Toronto Convention Centre on Saturday, October 20\. Interested readers can register

[here](https://secure.moneyshow.com/msc/toms/registration.asp?sid=TOMS12&scode=029492)

.