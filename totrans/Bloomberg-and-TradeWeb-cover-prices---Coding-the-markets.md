<!--yml
category: 未分类
date: 2024-05-12 19:38:55
-->

# Bloomberg and TradeWeb cover prices | Coding the markets

> 来源：[https://etrading.wordpress.com/2009/09/23/bloomberg-and-tradeweb-cover-prices/#0001-01-01](https://etrading.wordpress.com/2009/09/23/bloomberg-and-tradeweb-cover-prices/#0001-01-01)

## Bloomberg and TradeWeb cover prices

### September 23, 2009

I got an email query on cover prices for RFQs after my last post, so I went back to some old analysis of RFQs I did in 2006 to check. My code was getting the cover price from ION MarketView’s trading chain for the RFQs that traded with us on Bloomberg and TradeWeb. If the client traded away, with another dealer, or rejected, we would see a cover price of zero. This asymmetry allows a dealer to calculate excess winning margins for RFQs won, but not to see how far off the best price the dealer is for RFQs that trade away.

The excess winning margin is the difference between a winning price and the cover price. If the gap is too great, then maybe the dealer is suffering from a form of the [winners curse](http://en.wikipedia.org/wiki/Winner's_curse). The obvious response is to make pricing less aggressive. But the fact that losing dealers in an RFQ don’t see the winning price deters that. In the face of that asymmetry the right solution is probably to have real time feedback between hit ratios and pricing aggression…