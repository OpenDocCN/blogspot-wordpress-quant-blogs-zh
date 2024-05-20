<!--yml
category: 未分类
date: 2024-05-12 18:59:39
-->

# Quantitative Trading: Nonlinear Trading Strategies

> 来源：[http://epchan.blogspot.com/2013/05/nonlinear-trading-strategies.html#0001-01-01](http://epchan.blogspot.com/2013/05/nonlinear-trading-strategies.html#0001-01-01)

I have long been partial to

[linear strategies](http://epchan.blogspot.ca/2011/04/many-facets-of-linear-regression.html)

due to their simplicity and relative immunity to overfitting. They can be used quite easily to profit from mean-reversion. However, there is a serious problem: they are quite

[fragile](http://epchan.blogspot.ca/2013/03/what-can-quant-traders-learn-from.html)

,

*i.e.*

vulnerable to tail risks. As we move from mean-reverting strategies to momentum strategies, we immediately introduce a nonlinearity (stop losses), but simultaneously remove certain tail risks (except during times when markets are closed). But if we want to enjoy anti-fragility and are going to introduce nonlinearities anyway, we might as well go full-monty, and consider options strategies. (It is no surprise that Taleb was an options trader.)

It is easy to see that options strategies are nonlinear, since options payoff curves (value of an option as function of underlying stock price) are plainly nonlinear. I personally have resisted trading them because they all seem so complicated, and I abhor complexities. But recently a reader recommended a little book to me: Jeff Augen's "

[Day Trading Options](http://www.amazon.com/dp/0137029039/ref=as_li_qf_sp_asin_til?tag=quantitativet-20&camp=14573&creative=327641&linkCode=as1&creativeASIN=0137029039&adid=13WZN3EAQWT423HNK9FD&&ref-refURL=http%3A%2F%2Fepchan.blogspot.ca%2F)

" where the Black-Scholes equation (and indeed any equation) is mercifully absent from the entire treatise. At the same time, it is suffused with qualitative ideas. Among the juicy bits:

1) We can find distortions in the 2D implied volatility surface (implied volatility as z-axis, expiration months as x, and strike prices as y) which may mean revert to "smoothness", hence presenting arbitrage opportunities. These distortions are present for both stock and stock index options.

2) Options are underpriced intraday and overpriced overnight: hence it is often a good idea to buy them at the market open and sell them at market close (except on some special days! See 4 below.). In fact, there are certain days of the week where this distortion is the most drastic and thus favorable to this strategy.

3) Certain cash instruments have unusually high kurtosis, but their corresponding option prices consistently underprice such tail risks. Thus structures such as strangles or backspreads can often be profitable without incurring any left tail risks.

4) If there is a long weekend before expiration day (e.g. Easter weekend),  the time decay of the options value over 3 days is compressed into an intraday decline on the last trading day before the weekend.

Now, as quantitative traders, we have no need to take his word on any of these assertions. So, onward to backtesting!

(For those who may be stymied by the lack of affordable historical intraday options data, I recommend Nanex.net.)

===

There are still 2 slots available in my online

[Mean Reversion Strategies](http://www.epchan.com/my-workshops/)

workshop in May. The workshop will be conducted

*live*

via Adobe Connect, and is limited to a total of 4 participants. Part of the workshop will focus on how to avoid getting hurt when a pair or a portfolio of instruments stop cointegrating.