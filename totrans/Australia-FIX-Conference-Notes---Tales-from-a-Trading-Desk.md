<!--yml
category: 未分类
date: 2024-05-18 05:59:52
-->

# Australia FIX Conference Notes | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/10/16/australia-fix-conference-notes/#0001-01-01](https://mdavey.wordpress.com/2013/10/16/australia-fix-conference-notes/#0001-01-01)

## Australia FIX Conference Notes

I’m at the Australia FIX [conference](http://www.fix-events.com/Australia/Agenda.html) today in Sydney.

Exhibition area vendors should consider the benefit of User Experience involvement in their applications/demo’s.  I realise numerous vendors sell non-UI technology, but the demo’s really could do with some work to allow potential customers to clear understand the value add from the data ROI opportunity.

Few interest take away from the chatter and usual select of finance magazine available at these conferences:

*   Multi asset TCA – FX harder than equities.
*   Hong Kong flow directs lot of flow to Australia
*   Equity Market Trading System of Borsa Istanbul, as of March 31, 2013, throughput of almost 5k orders/second and  latency at  peak time of order flow below 1 millisecond via FIX interface
*   Aquis Exchange – designated market maker making a two-way price consistently in the market, passive orders submitted, and any order or message, doesn’t count as a message.  Non-designated market marker and designated market makers can send up to 25k messages a day for £2.5k per month More than 25k msg/day, will incur a £10k per month charge.  As liquidity builds in steps from £10k-20k-30k and tops out at £50k per month
*   Battling the bottleneck: an analysis of the new Eurex [platform](http://www.automatedtrader.net/articles/analysis/144302/battling-the-bottleneck-an-analysis-of-the-new-eurex-platform)
*   Life in the [slow](http://www.automatedtrader.net/articles/exchange-views/144193/life-in-the-slow-lane) lane – speed bumps to level the latency game.  EBS Live market data costs are about $50k per month which sends updates on incoming orders and prices every 100 milliseconds.  33 milliseconds for data to travel between London and New York, thus a speed bump of anything over 30 milliseconds opens up arbitrage opportunities from a geographic location perspective.
*   Multicast delivery of market data.
*   Ditch HSRP (hot standby router protocol), lose 1.5 milliseconds. Drop NAT (network address translation) and gain another 500 microseconds.
*   Smart order routing venue access sequence is important
*   What information is key to empower the buy-side trader – Thomas S. Kingsley, Head of APAC Execution Consulting and Trading, Bloomberg Tradebook
*   Algo Strategies – IS, VWAP, TWAP, Target Close, Participation/With Volume, Dark Aggregation/interaction/Liquidity-driven/Signal-driven, custom
*   Some brokers are offering the ability to look into the algo, and see what its doing in real-time or post trade – Jason Lapping, Head of Asia Paciﬁc Trading, Dimensional (Australia)
*   Future: Adaptive algo, leverage statistical analysis to look ahead for the strategy – Thomas S. Kingsley, Head of APAC Execution Consulting and Trading, Bloomberg Tradebook

Keynote Speech: A Seismic Shift in Markets? Are You Ready? – Seth Merrin, CEO and Founder, Liquidnet:

*   Nice slide deck – apart from some of the chart images
*   Great Rotation from rise in interest rates
*   Asset allocation “You can invest into equities, and possibly loose money, or invest in fixed income and definitely loose money”
*   Regulation can be a constraint or an enabler
*   Market structure by design or default – USA is default.  Australia leading by example – market structure, investing for the future.
*   Dark pools created for anonymity, size and price improvements for the wholesale market
*   More Efficient Market = price discovery + size discovery

FX Transaction Cost Analysis (TCA):

*   What benchmark to use for FX?  High/low of the day? Over time high/low?
*   VWAP/TWAP may also be appropriate benchmark for [TCA](http://www.fxweek.com/fx-week/feature/2183429/standards-multiply-tca-takes-hold)
*   Unlike equities, FX complicated by custodian (execution performance).  Also, what is the definition of a trading day in FX land? Would the custodian in a different region have a different trading day?
*   Possible solution to FX TCA Spot – [bucket](http://www.e-forex.net/articles/free/Special+Report/1852/Introducing+benchmarks+into+the+FX+trade+execution+process) trades: unrestricted currencies, restricted currencies via custodians, FX execution via custodians
*   Performance analytics – helping to bring [transparency](http://www.financial-journalist.co.uk/financial_journalist/finance/performance-analytics-helping-to-bring-transparency-to-the-fx-pricing-process/) to the FX pricing process

~ by mdavey on October 16, 2013.

Posted in [Trading](https://mdavey.wordpress.com/category/trading/)
Tags: [TCA](https://mdavey.wordpress.com/tag/tca/)