<!--yml
category: 未分类
date: 2024-05-12 19:50:37
-->

# Market orders and limit orders | Coding the markets

> 来源：[https://etrading.wordpress.com/2006/09/07/market-orders-and-limit-orders/#0001-01-01](https://etrading.wordpress.com/2006/09/07/market-orders-and-limit-orders/#0001-01-01)

## Market orders and limit orders

### September 7, 2006

In chapter 14, [Harris](http://www.tradingandexchanges.com) has a marvellously clear explanation of the interplay between market and limit orders. To simplify massively, imagine an order book with a very sparse flow of market orders. Traders placing limit orders on that book will have to improve on the prices of the existing limit orders to become top of book, and match with one of the rare market orders. But in doing so, they’ll narrow the spread between best bid and ask. As the spread gets narrower, market orders will trade at better prices, causing market order flow to increase, and spreads to widen. As spreads widen, market order prices worsen, making limit order based strategies more attracive. And so the system is in dynamic equilibrium.