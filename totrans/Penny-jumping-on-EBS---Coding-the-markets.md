<!--yml
category: 未分类
date: 2024-05-12 19:33:55
-->

# Penny jumping on EBS | Coding the markets

> 来源：[https://etrading.wordpress.com/2012/09/20/penny-jumping-on-ebs/#0001-01-01](https://etrading.wordpress.com/2012/09/20/penny-jumping-on-ebs/#0001-01-01)

## Penny jumping on EBS

### September 20, 2012

[EBS](http://www.ebs.com/) is an FX ECN owned and operated by [ICAP](http://www.icap.com/), a cash FX equivalent to [Bloomberg](http://www.bloomberg.com/) or [TradeWeb](http://www.tradeweb.com/). It’s been in decline for some time as flow shifts to single dealer platforms. Here’s an interesting [NY Times article](http://www.nytimes.com/reuters/2012/09/20/business/20reuters-forex-companies-ebs.html "Thanks to ALEA for the link!") on how introducing an extra decimal place in their prices resulted in a fall in trading volumes. It’s an interesting illustration of how market microstructure choices can affect participant behaviour. A key phrase in the article is: “But that fifth decimal attracted super-fast computer traders, often disrupting the flow of liquidity on the EBS platform”

So how did the high speed traders disrupt the flow of liquidity ? Note that EBS’s cash FX trading is organised as a [limit order book](http://www.ebs.com/markets/spot-fx.aspx).  Introducing an extra decimal creates 10 times as many price levels in the order book, which in turn makes [penny jumping](http://en.wikipedia.org/wiki/Front_running "Penny jumping") much easier for quick automated trading strategies. Which is obviously going to piss off the other market participants, who end up paying the spread earned by the penny jumpers. Larry Harris has an excellent discussion of penny jumping it in his seminal “Trading and Exchanges”, but the Wikipedia link has an adequate explanation.

No doubt considerations like the ones above motivated the rates dealers making govt bond markets on MTS when they decided not to admit hedge funds.