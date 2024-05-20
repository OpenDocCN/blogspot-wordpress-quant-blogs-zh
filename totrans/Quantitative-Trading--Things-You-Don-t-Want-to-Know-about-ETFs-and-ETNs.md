<!--yml
category: 未分类
date: 2024-05-12 18:56:25
-->

# Quantitative Trading: Things You Don't Want to Know about ETFs and ETNs

> 来源：[http://epchan.blogspot.com/2016/06/some-things-you-dont-want-to-know-about.html#0001-01-01](http://epchan.blogspot.com/2016/06/some-things-you-dont-want-to-know-about.html#0001-01-01)

Everybody loves trading or investing in ETPs. ETP is the acronym for exchange-traded products, which include both exchange-traded funds (ETF) and exchange-traded notes (ETN). They seem simple, transparent, easy to understand. But there are a few subtleties that you may not know about.

1) The most popular ETN is VXX, the volatility index ETF. Unlike ETF, ETN is actually an

*unsecured*

bond issued by the issuer. This means that the price of the ETN may not just depend on the underlying assets or index. It could potentially depend on the credit-worthiness of the issuer. Now VXX is issued by Barclays. You may think that Barclays is a big bank, Too Big To Fail, and you may be right. Nevertheless, nobody promises that its credit rating will never be downgraded. Trading the VX future, however, doesn't have that problem.

2) The ETP issuer, together with the "Authorized Participants"  (the market makers who can ask the issuer to issue more ETP shares or to redeem such shares for the underlying assets or cash), are supposed to keep the total market value of the ETP shares closely tracking the NAV of the underlying assets. However, there was one notable instance when the issuer deliberately not do so, resulting in big losses for some investors.

That was when the issuer of TVIX, the leveraged ETN that tracks 2x the daily returns of VXX, stopped all creation of new TVIX shares temporarily on February 22, 2012 (see 

[sixfigureinvesting.com/2015/10/how-does-tvix-work/](http://sixfigureinvesting.com/2015/10/how-does-tvix-work/)

). That issuer is Credit Suisse, who might have found that the transaction costs of rebalancing this highly volatile ETN were becoming too high. Because of this stoppage, TVIX turned into a closed-end fund (temporarily), and its NAV diverged significantly from its market value. TVIX was trading at a premium of 90% relative to the underlying index. In other words, investors who bought TVIX in the stock market by the end of March were paying 90% more than they would have if they were able to buy the VIX index instead. Right after that, Credit Suisse announced they would resume the creation of TVIX shares. The TVIX market price immediately plummeted to its NAV per share, causing huge losses for those investors who bought just before the resumption.

3) You may be familiar with the fact that a β-levered ETF is supposed to track only β times the

*daily*

returns of the underlying index, not its long-term return. But you may be less familiar with the fact that it is also not supposed to track β times the

*intraday*

return of that index (although at most times it actually does, thanks to the many arbitrageurs.)

Case in point: during the May 2010 Flash Crash, many inverse levered ETFs experienced a

*decrease*

in price as the market was crashing downwards. As inverse ETFs, many investors thought they are supposed to

*rise*

in price and act as hedge against market declines. For example, this

[comment letter](https://t.co/DilS8kZ8X1)

to the SEC pointed out that DOG, the inverse ETF that tracks -1x Dow 30 index, went

*down*

more than 60% from its value at the beginning (2:40 pm ET) of the Flash Crash. This is because various market makers including the Authorized Participants for DOG weren't making markets at that time. But an equally important point to note is that at the end of the trading day, DOG did return 3.2%, almost exactly -1x the return of DIA (the ETF that tracks the Dow 30). So it functioned as advertised. Lesson learned: We aren't supposed to use inverse ETFs for intraday nor long term hedging!

4) The NAV (not NAV

*per share*

) of an ETF does not have to change in the same % as the underlying asset's unit market value. For example, that same

[comment letter](https://t.co/DilS8kZ8X1)

I quoted above wrote that GLD, the gold ETF, declined in price by 24% from March 1 to December 31, 2013, tracking the same 24% drop in spot gold price. However, its NAV dropped 52%. Why? The Authorized Participants redeemed many GLD shares, causing the shares outstanding of GLD to decrease from 416 million to 266 million.  Is that a problem? Not at all. An investor in that ETF only cares that she experienced the same return as spot gold, and not how much assets the ETF held. The author of that comment letter strangely wrote that "Investors wishing to participate in the gold market would not buy the GLD if they knew that a price decline in gold could result in twice as much underlying asset decline for the GLD." That, I believe, is nonsense.

For further reading on ETP, see

[www.ici.org/pdf/per20-05.pdf](http://www.ici.org/pdf/per20-05.pdf)

and

[www.ici.org/pdf/ppr_15_aps_etfs.pdf](http://www.ici.org/pdf/ppr_15_aps_etfs.pdf)

.

===

**Industry Update**

Alex Boykov co-developed the

[ WFAToolbox](http://wfatoolbox.com/?utm_source=epchan&utm_medium=paid&utm_campaign=Articles)

– Walk-Forward Analysis Toolbox for MATLAB, which automates the process of using a

*moving*

window to optimize parameters and entering trades only in the out-of-sample period. He also compiled a standalone application from MATLAB that allows any user (having MATLAB or not) to upload quotes in csv format from Google Finance for further import to other programs and for working in Excel. You can download it here:

[wfatoolbox.com/epchan](http://wfatoolbox.com/epchan)

.

**Upcoming Workshop**

AI/machine learning techniques are most useful when someone gives us newfangled technical or fundamental indicators, and we haven't yet developed the intuition of how to use them. AI techniques can suggest ways to incorporate them into your trading strategy, and quicken your understanding of these indicators. Of course, sometimes these techniques can also suggest unexpected strategies in familiar markets.

My course covers the basic AI techniques useful to a trader, with emphasis on the many ways to avoid overfitting.