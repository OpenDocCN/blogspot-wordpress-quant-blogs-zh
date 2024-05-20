<!--yml
category: 未分类
date: 2024-05-12 19:52:57
-->

# Market structure | Coding the markets

> 来源：[https://etrading.wordpress.com/2006/06/08/market-structure/#0001-01-01](https://etrading.wordpress.com/2006/06/08/market-structure/#0001-01-01)

## Market structure

### June 8, 2006

The fixed income [ECNs](http://www.sec.gov/answers/ecn.htm) are either quote driven or order driven markets. [Bloomberg](www.bloomberg.com) and [TradeWeb](www.tradeweb.com) are the leading quote driven markets, and [Liffe](http://www.euromts-ltd.com/) is an example of an order driven market. [MTS](http://www.euromts.com/) is a curious hybrid.

In an order driven market, an order on one side of the order book for an instrument can potentially match with any order on the other side of the book, given the usual provisos about size and price. In a quote driven market, a trader wanting to buy or sell will request a quote from the dealers quoting on the ECN by clicking on a price.

The key difference is that on a quote driven market, a trader looking to buy or sell can only trade with a dealer. On an order driven market, that trader potentially trades with any market participant. Let's put that another way: on a quote driven market, only dealers supply liquidity. On an order driven market, all participants with orders in the market are supplying liquidity.

As [Harris](http://www.tradingandexchanges.com) astutely points out, the key factor is the cost of liquidity. Dealers supply liquidity to the market, and the cost they charge is the spread. If you want to sell, you can only trade at a dealer's bid price in a quote driven market. In an order driven market, you can place your sell order at any price. However, if you want the order filled quickly, you'd better place it somewhere near the top of book.

So in an order driven market, there's potentially more liquidity, and so, from a dealer perspective, spreads will be narrower. Ergo dealers prefer quote driven markets.

Why would buy side traders prefer quote driven markets, if they're paying more for the dealer supplied liquidity ?  For one, they don't have to manage an order on the market. And on multi dealer ECNs with RFQs that work as competitive auctions, they should be able to minimise the spread.