<!--yml
category: 未分类
date: 2024-05-12 23:36:25
-->

# Front-Run The Delta: How Knight Makes a Market: Evidence from RWE Group

> 来源：[https://frontrunthedelta.blogspot.com/2011/07/how-knight-makes-market-evidence-from.html#0001-01-01](https://frontrunthedelta.blogspot.com/2011/07/how-knight-makes-market-evidence-from.html#0001-01-01)

Fond of trading on the

[OTC Bulletin Board](http://www.otcbb.com/)

, among other prominent markets,

[Knight Capital](http://www.knight.com/)

"trades or

[makes a market](http://www.knight.com/ourFirm/vsMVS.asp)

in over 19,000 U.S. Equities" according to their website.  The goal of this post, and I hope those going forward, is to examine the science behind Knight's activities.

The example today is

[RWE Group](http://www.rwe.com/web/cms/en/10122/rwe/rwe-group/)

.  What they do and how they do it is wholly unimportant for this exercise.  The important and relevant data points to build on today are price and time.  Price for RWE quoted in Euros, RWEOY quoted in US dollars, the EUR/USD interbank rate, and the

[synchronized](http://www.highfrequencytraders.com/article/820/major-upgrade-fsmlabs-timekeeper-increases-time-precision-high-frequency-trading)

time stamps for all 3 variables.

**Outrights**

: The two stocks together.  

[RWE](http://www.interactivebrokers.co.uk/contract_info/v3.5/index.php?action=Details&site=IB&conid=14198&detlev=2&sess=1310425144)

 (blue/red) is denominated in Euros and opens at 02:00AM while

[RWEOY](http://www.interactivebrokers.co.uk/contract_info/v3.5/index.php?action=Details&site=IB&conid=58593713&detlev=2&sess=1310425201)

 (green/purple), denominated in US dollars, does not open until 08:30AM, despite a relatively tight bid/ask for the prior hour.  The chart below is April 8, 2011, from left to right, 2:00AM CST to 3:00PM CST.

**Currency**

: The EUR/USD interbank currency rate available via IB's

[Idealpro](http://www.interactivebrokers.com/en/trading/exchanges.php?exch=ibfxpro&showcategories=&ib_entity=llc)

.  The currency was recorded simultaneously with the two stocks to avoid using potentially stale quotes.

EUR/USD - 8 April, 2:00AM to 3:00PM CST

**Implied Value.**

Using the price of the shares denominated in Euros and the live EUR/USD exchange rate, a theoretical value for the USD-listed shares can be derived.  

[Gagnon and Karolyi (2004)](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=577004)

provide an exhaustive study into this relationship.  The authors study 

589 pairs of dual-listed stocks from 39 countries using daily closing prices from 1990 to 2002\.  While most pairs are found to stay within a 15 to 20 basis point (.15% to .2%) range with one another, the authors note that "the premium on the cross-listed shares relative to home-market shares can be as large as [66 percent](http://quotes.nasdaq.com/asp/SummaryQuote.asp?symbol=INFY&selected=INFY) and the discounts as large as [87 percent](http://www.adrbnymellon.com/files/TN7963.pdf)," but deviations of such magnitude were found to last no longer than one day.""Deviations from price parity,” they suggest, “their persistence over time and the excess comovements are related to country-level and firm-specific attributes that reflect, not only institutional impediments to arbitrage, but also informational barriers in the form of information asymmetries among different investors and the presence of [noise traders](http://en.wikipedia.org/wiki/Noise_trader)."  They find that "excess comovements are significantly related to the fraction of global trading that takes place in the U.S. markets." [Ejara and Ghosh (2004)](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1560482) support their findings and provided important research into the field.

Below is the implied value of RWE priced in USD combined with the live quoted price of RWEOY duly listed in USD. The market for RWEOY is most robust during the overlapping hours when market making firms are able to more easily transfer risk from one market to the other. The bid/ask spread of RWEOY after the European closing (on the right of the chart) is evidence of this mechanism.

April 8, 2011

July 15, 2011

Finding the difference between the synthetic value of RWE and the real value of the RWEOY is the arbitrage. In this case, as in 

[others](http://frontrunthedelta.blogspot.com/2011/07/etf-futures-arbitrage-fxb-and-gbp.html)

, dynamic inventory and risk management systems must be in place for the pricing participants.

**Overlapping Market Spreads.**

April 8, 2011 

July 15, 2011

Further Reading: