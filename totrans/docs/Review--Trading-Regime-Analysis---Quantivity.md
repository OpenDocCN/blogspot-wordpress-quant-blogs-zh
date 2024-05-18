<!--yml
category: 未分类
date: 2024-05-18 13:54:12
-->

# Review: Trading Regime Analysis | Quantivity

> 来源：[https://quantivity.wordpress.com/2010/01/24/review-trading-regime-analysis/#0001-01-01](https://quantivity.wordpress.com/2010/01/24/review-trading-regime-analysis/#0001-01-01)

![](img/d46e9b82bb76b7bb8bc764416356b601.png "trading-regime-analysis-cover") The following is a review of Trading Regime Analysis by Gunn, consistent with Quantivity’s on-going market regime theme and in response to reader request.

Readers seeking rigorous quantitative treatment of regime analysis will be disappointed (as frequently and gleefully acknowledged by the author), as the text seeks to analyze regimes primarily through anecdotal behavioral finance and an idiosyncratic basket of technical analysis. That said, the text *builds intuition and ultimately endorses numerous intellectual themes which similarly underlie rigorous quantitative analysis of market regimes*.

This is admittedly an unexpected curiosity. Thus, value lies in observing how this regime intuition is framed by a certified technical analyst, voyeuristically from the perspective of a quant. Despite TA arguably serving as the intellectual ancestor of quantitative analysis (as introduced in [Why Moving Averages](https://quantivity.wordpress.com/2010/01/08/why-moving-averages/)), very rarely do technical and modern quantitative analyses converge on intuition. As with any intellectual juxtaposition, such curiosity merits study.

The points of juxtaposed intuition are as follows, several of which are quite remarkable admissions for a classic technical analyst (despite being widely held by quants):

*   Futility of deterministic prediction: “‘prediction’, as we commonly think of it, is a totally impossible and futile exercise” (p. 3)
*   No holy grail: “realisation that ‘everything works but only some of the time’ is, in my opinion, crucial for long-term success or survival in the financial trading market place.” (p. 7)
*   Ternary regime classification (trend, range, or indeterminate): “market can do one of three things. It can trend, it can trade in a general range or it can do a little bit of both.” (p. 15)
*   Probabilistic regime prediction: “purpose of regime trading analysis is to identify what trading environment the market is in and, crucially, to identify when it is *probable* that the market is about to enter either a trending or range-trading regime” (p. 15)
*   Behavioral finance: selected psychological and sociological tenets of behavioral finance are covered, including cognitive dissonance (p. 28), “greater fool theory” (p. 38), bounded rationality (p. 40), and market psychology (p. 73)
*   Centrality of volatility: role of volatility in driving regime evolution is posited in Chapter 3, including numerous subtleties partially re-purposed from the quantitative world: equilibria (p. 45), realized volatility (p. 51), volatility clustering (p. 54), implied volatility (p. 55), relative value (p. 57), and vol of vol (p. 65)
*   Price range and regimes: “most important section of the book” (p. 60) explains regimes are driven by volatility measured in context of *price ranges* (as measured by standard deviation), rather than velocity of price changes; despite lack of analytic rigor, many quant strategies are conceptually similar to the intuition illustrated in Figure 3.12

Having expressed those insights across Part I, the book then goes on for nearing 200 pages in Part II rehashing an idiosyncratic basket of technical analysis techniques: orthodox pattern recognition, candlesticks, volume considerations, previous high/low, Elliot waves, moving averages, Bollinger bands, ADX, point/figure charts, change/divergence rates, Williams %R, and Donchian. Incredible cognitive juxtaposition discussing [Vanna](http://en.wikipedia.org/wiki/Greeks_%28finance%29#Vanna) and Elliot waves in the same book (in fact, unique, in the Quantivity library).

Part III again juxtaposes basic analysis of option vol surfaces (Chapters 17 and 18) with a few technical trend-following indicators (Chapters 19 and 20). Chapter 21 introduces a new indicator (obligatory for any TA book), almost in passing, named Trading Regime Indicator (p. 292):

> TRI is calculated by taking the standard deviation of a price series, taking a moving average of that standard deviation, and examining the gap between the two.

Gunn seeks to weave the story cohesively together in Chapter 22, introducing a “trading regime grid” (p. 301). Readers familiar with the quant blogosphere will find remarkable *conceptual* similarity between this grid of technical indicators and various quantitative “state of the market” summaries (including the proposed [Market Regime Dashboard](https://quantivity.wordpress.com/2009/08/23/market-regime-dashboard/)).

Finally, Gunn summarizes in Chapter 26, with two particularly fascinating quotes. First, a reductionist restatement of trading regime analysis (p. 389):

> Is trading regime analysis just a fancy way of saying something that has had a big, fast move will probably slow down and either reverse or trade in a range, or something that has not moved for some time will probably have a big move soon? Well, to be perfectly honest, yes it is.”

Juxtaposed with proposing a hybrid technical-economic methodology called “techonomic analysis” (p. 390):

> Surely it is worth asking the question…of whether it is possible to combine a systematic, mechanical entry and exit method with a discretionary evaluation of position size and risk.”

With possible exception of discretionary position sizing, one can imagine retail quant traders asking similar questions of their own strategies. For a trend-following technical analyst who particularly likes Elliot waves, this is indeed a fascinating juxtaposition.