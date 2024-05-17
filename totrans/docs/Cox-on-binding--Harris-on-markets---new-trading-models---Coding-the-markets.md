<!--yml
category: 未分类
date: 2024-05-12 19:48:38
-->

# Cox on binding, Harris on markets & new trading models | Coding the markets

> 来源：[https://etrading.wordpress.com/2007/01/09/cox-on-binding-harris-on-markets-new-trading-models/#0001-01-01](https://etrading.wordpress.com/2007/01/09/cox-on-binding-harris-on-markets-new-trading-models/#0001-01-01)

## Cox on binding, Harris on markets & new trading models

### January 9, 2007

Back in 1990, Brad Cox wrote a far sighted paper on software components, static and dynamic binding technology, and their implications for software reuse: [Planning the Software Industrial Revolution](http://www.virtualschool.edu/cox/pub/PSIR/). Mainstream software practitioners still haven’t assimilated Cox’s contention that static and dynamic binding are equally valid techniques appropriate at different places in software architecture. Many seem to think the [two are polar opposites, and one must pick sides](http://www.mindview.net/WebLog/log-0052), rather than being complementary. Which is probably a symptom of the fact that it’s still early days for mixed language development environments.

In 80s Britain there was a similar debate on market economies versus comand and control, socialist, economies. Market economics won out of course, and that result was validated by the collapse of the Soviet Union at the end of the decade. More recently, the debate on the applicability of markets has moved from the national macroeconomic scale of the 80s debate to the level of individual business organisations. Some advocate [prediction markets](http://http://en.wikipedia.org/wiki/Decision_market) as a better means of internal organisation than traditional command and control. Apparently [Google](http://www.google.com) and [Microsoft](http://www.microsoft.com) use them internally. The NHS introduced [internal markets](http://www.nhs.uk/England/AboutTheNhs/History/1988To1997.cmsx), with mixed results.

In chapter 9 of [Trading & Exchanges](http://www.tradingandexchanges.com), Harris points out that “not all economic decisions are best made in the marketplace. Markets work well only when the costs of negotiating are small relative to the costs of the goods or services that trade there. Markets work poorly when transaction costs are large or when activities need to be highly coordinated….Companies are the most important command organizations within a market economy. People form companies that managers control in order to avoid the excessive market negotiation costs.”

Markets are like dynamic binding or loose coupling. And command and control is like static binding or tight coupling. They’re both useful, applicable and appropriate in different circumstances. Monopolies and socialist economies impose static binding where dynamic binding does the job better. And I suspect [some of the outsourcing deals](http://www.finextra.com/fullstory.asp?id=13203) impose loose coupling where tight works better.

Recently [Holky has covered the contention by Icap](http://http://mostly.wordpress.com/2006/12/04/epda-attacks-government-bond-market-restrictions) and others that MTS is a monopoly. And he’s also discussed [new transaction types](http://mostly.wordpress.com/2006/11/30/bond-market-resists-algorithmic-trading/) and the shortcomings of the quote driven RFQ model. Quote driven markets like Bloomberg and TradeWeb impose a kind of tight binding in that those raising RFQs can only trade with dealers. Order driven markets, which show form executable prices, are more loosely coupled. Any participant can trade with any other. I suggest that any new trading model beyond the established quote and order driven ECNs must be loosely coupled to succeed. I wonder how loosely coupled LiqudityHub will be ?