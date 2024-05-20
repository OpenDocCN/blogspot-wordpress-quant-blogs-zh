<!--yml
category: 未分类
date: 2024-05-12 19:39:34
-->

# Order book resiliency | Coding the markets

> 来源：[https://etrading.wordpress.com/2009/06/16/order-book-resiliency/#0001-01-01](https://etrading.wordpress.com/2009/06/16/order-book-resiliency/#0001-01-01)

## Order book resiliency

### June 16, 2009

In Agressive Orders and the Resiliency of a Limit Order Market Degryse et al present an interesting study of the Paris Bourse order book reaction to incoming order types. They study how best bid/offer, spreads and depth evolve in reaction to incoming market and limit orders, and to what degree they revert. Their findings, which are based on data from 1998,  are intuitively plausible. For me the surprise came in seeing the authors note the average interval between best limit updates – in one case 84 seconds !  That seems like an eternity when compared to Eurex order books when the market is moving !