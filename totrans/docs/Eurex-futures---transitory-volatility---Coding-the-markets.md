<!--yml
category: 未分类
date: 2024-05-12 19:47:52
-->

# Eurex futures & transitory volatility | Coding the markets

> 来源：[https://etrading.wordpress.com/2007/03/29/eurex-futures-transitory-volatility/#0001-01-01](https://etrading.wordpress.com/2007/03/29/eurex-futures-transitory-volatility/#0001-01-01)

## Eurex futures & transitory volatility

### March 29, 2007

In ch 19 [Harris](http://www.tradingandexchanges.com) distinguishes between fundamental and transitory volatility. Fundamental volatility is due to unexpected changes in the fundamental values of instruments, and transitory volatility is due to impatient traders trading market orders. Bid/ask bounce is a form of transitory volatility. When you see bid/ask bounce in a market you’ll see the prices at the top of book tick up,down,up,down constantly, usually in a one tick range.

A good place to observe this in fixed income is Eurex futures. The front month contracts for Schatz, Bobl, Bund and Buxl (2,5,10,30 yrs) are the most heavily traded contracts in the Euro rates world. A lot of the trades on these contracts are hedges on cash bond positions. The traders hedging their cash  positions will take whatever prices are showing at the top N levels in order to hedge, so they match Harris’ characterisation of impatient market order traders.