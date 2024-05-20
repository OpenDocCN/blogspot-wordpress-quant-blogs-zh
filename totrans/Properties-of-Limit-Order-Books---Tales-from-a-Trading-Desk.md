<!--yml
category: 未分类
date: 2024-05-18 06:36:02
-->

# Properties of Limit Order Books | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2012/08/23/properties-of-limit-order-books/#0001-01-01](https://mdavey.wordpress.com/2012/08/23/properties-of-limit-order-books/#0001-01-01)

## Properties of Limit Order Books

Whilst [reading](http://fiquant.mas.ecp.fr/Pub/QMF2012.pdf) “Empirical and Mathematical Properties of Limit Order Books”, I came across “A [Family](https://www.assembla.com/spaces/MarketModel/wiki) of Financial Market Models”.  Although old, [FinancialMarketModel](https://www.assembla.com/spaces/MarketModel/wiki) is of interest for anyone interested in markets and order books since the wiki offer some appropriate reading material coupled with source [code](//subversion.assembla.com/svn/MarketModel/src/).  Possibly of most interest is the [player](https://www.assembla.com/spaces/MarketModel/wiki/GenericPlayer) functionality, and the DoubleAuctionOrderBook offering basic limit order processing:

> [DoubleAuctionOrderBook](https://www.assembla.com/wiki/show/MarketModel/DoubleAuctionOrderBook "DoubleAuctionOrderBook") behaves like a typical stock market. Some (patient) traders place limit orders which specify a quantity and price. Other (impatient) traders place market orders which execute immediately at the market price, provided that there is adequate liquidity provided by outstanding limit orders. As implemented, placing or cancelling a limit order takes log time, placing a market order takes constant time, and cleanup takes linear time, all w.r.t. the number of limit orders pending

Having been involved in a number of market projects over the years, although the FinancialMarketModel is limited to basic limit orders, the source code is at least public, and the player concepts are relevant to anyone coding there own market from an acceptance test perspective.  For those ambitious, this codebase could we consider in terms of adding [peg](www.euronext.com/fic/000/041/609/416094.pdf) orders (or similar) to being to model further market behavior – possibly considering cloning the NYSE Euronext order types.

~ by mdavey on August 23, 2012.

Posted in [Trading](https://mdavey.wordpress.com/category/trading/)
Tags: [OrderBook](https://mdavey.wordpress.com/tag/orderbook/)