<!--yml
category: 未分类
date: 2024-05-12 19:01:55
-->

# Quantitative Trading: High-frequency trading in the foreign exchange market

> 来源：[http://epchan.blogspot.com/2012/03/high-frequency-trading-in-foreign.html#0001-01-01](http://epchan.blogspot.com/2012/03/high-frequency-trading-in-foreign.html#0001-01-01)

This is the title of a

[report](http://www.bis.org/publ/mktc05.pdf)

published by the Bank of International Settlements (which serves central banks around the world) in September 2011\. As a Forex trader myself, I of course peruse it with great interest hoping to glimpse whatever is the state-of-the-art. Here are a few interesting nuggets, together with my commentary:

1) FX HFT operate with a latency of less than 1 ms, while most of us mere algorithmic traders typically suffer a latency of at least 10ms.  For example, Interactive Brokers does not yet provide collocation facilities for its customers, so the best we can do is to place our trading servers on the internet backbone close to its Stamford, CT, location. The best round-trip ping time is 10ms. Those who trade with FXCM may have a better chance for lower latency, as they provide

*free*

collocation to their clients. Those who trade on the ECN FXall can

[collocate at their Equinix data center](http://www.equinix.com/company/news-and-events/press-releases/americas/2009/fxall_offers_foreign_exchange_platform_en/)

, while

[FCM360](http://www.fcm360.com/financial-industry-solutions/foreign-exchange-hosting-colocation-connectivity/icap-ebs-servers/)

provides collocation service to EBS traders. I cannot find any collocation service for Hotspot FX or Currenex. If you know of such services, or FX brokers who provide collocation, do leave a comment!

2) HFT typically operate in markets with high liquidity and low volatility. The former is not surprising, since markets with low liquidity has few counter-parties to take advantage of. The latter requires a bit of nuance. I think most HFT would benefit from high volatility in a mean-reverting market, but unfortunately high volatility is usually correlated with market in a free fall. So don't be surprised if you find that HFT-provided liquidity suddenly disappears when the market is in stress, though the BIS report stated that they are also quick to re-enter the market once the turmoil is over.

3) As a corollary of 2), HFT mostly trade in the major currency pairs. But increasingly, NZD and MXN have drawn many automated and HF traders.

4) Almost by definition, the bid/ask quotes placed by HFT tend to remain on the book for a very short time, measured in ms, unless forced by the exchange to stay longer. EBS and Reuters both has minimum quote life or minimum fill ratio. One exchange that does

*not*

 have such minimums is Currenex, which is therefore particularly attractive to HF trading. Hence if you are not a HF player, and do not wish to be taken advantage of  by a HF player, be wary of Currenex!

5) Two of the favourite categories of HFT strategies: triangle arbitrage and liquidity-redistribution (taking advantage of pricing discrepancies across different trading platforms.) Despite the bad reputation HFTers have been acquiring in the last few years, I think they do provide a useful service to other algo traders like myself via these 2 strategies. It is a hassle to keep looking for a better broker/prices for your strategy!