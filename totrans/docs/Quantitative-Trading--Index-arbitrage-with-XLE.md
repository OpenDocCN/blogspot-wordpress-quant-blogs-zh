<!--yml
category: 未分类
date: 2024-05-12 19:24:46
-->

# Quantitative Trading: Index arbitrage with XLE

> 来源：[http://epchan.blogspot.com/2007/02/in-looking-for-pairs-of-financial.html#0001-01-01](http://epchan.blogspot.com/2007/02/in-looking-for-pairs-of-financial.html#0001-01-01)

In looking for pairs of financial instruments to pair trade, we do not have to limit ourselves to pairs that occur in "nature". We can often construct our own baskets of stocks to trade against an index (or an ETF representing this index). In fact, such pairs usually show better cointegration properties than any stock or ETF pairs. I have alluded to this index arbitrage idea in an earlier

[post](http://epchan.blogspot.com/2007/02/mr_05.html "post")

, and the details of the methodology are explained in my

[articles for Subscribers](http://epchan.com/subscriptions.html "articles for Subscribers")

. I tried this strategy on favorite sector ETF: the energy SPDR XLE.

XLE is composed of some 33 stocks (as of 2/16/2007). Our goal is to pick some smaller subset of these stocks to form a basket. We pick them based on how well they cointegrate with XLE. How big should this subset be? The higher the number, the better this basket cointegrates with XLE, but the smaller the profits. (If you include all stocks in XLE in this basket, then the basket cointegrates perfectly with XLE, but there will be no trading opportunities!) The lower the number, the higher the (specific) risk as well as return. So it is more of a personal risk-return preference than any scientific criterion which determines how many stocks to pick. I pick a basket with 10 stocks. I have found that this basket cointegrates with XLE with better than 99% probability since 2001/05/22\. The

[half-life](http://epchan.blogspot.com/2007/01/what-is-your-stop-loss-strategy.html "half-life")

for mean-reversion is about 20 days, which means you have to hold a position for at most a quarter. (My own rule is to exit when the spread hasn't reverted in 3 times the half-life.) If you enter into a position when the z-score is about ±2, you can expect a profit of about $2,000 on an investment of about $58,000 on one side. This comes to a return per trade of about 3%. You can of course boost this return by using options to implement the XLE position instead.

As an aside, if you use Interactive Brokers, you can easily trade an entire basket of stocks using their Basket Trader.

I have created an online spreadsheet with (almost) real-time values of this spread in the

[subscription area](http://epchan.com/subscriptions.html "subscription area")

. (The detailed composition of this basket of 10 stocks are also described there.) Note that in theory, every time the XLE changes composition, we will have to re-compute our basket composition as well. But fortunately XLE composition does not change very much or very often, so I will only update my basket at most once a month.

[![](img/bd0a4261d0263c63a7cefab5497f966e.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj2YZcqsZKHxyHLMFr1cZNaaXS3Lb8pawzzeoqrRZxIv2G9jdfaUsoZjmDHG81UgAP7_Nac1TWISQ75MXNFgQA_8UckLfBKbeZCplO0AtybzYwru7oBV_WiLW7st1JwBtALJGca0A/s1600-h/XLE.bmp)