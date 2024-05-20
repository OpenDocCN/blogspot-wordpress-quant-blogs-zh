<!--yml
category: 未分类
date: 2024-05-18 13:54:26
-->

# Causality, Exogeny & Regimes | Quantivity

> 来源：[https://quantivity.wordpress.com/2010/01/10/causality-exogeny-regimes/#0001-01-01](https://quantivity.wordpress.com/2010/01/10/causality-exogeny-regimes/#0001-01-01)

An assumption of modern financial economics is of *fundamental causality*: effects in electronic financial markets are primarily due to causes in the “real world”. Classic examples are earnings announcements and GDP numbers, for micro (equities) and macro (fx) respectively. For many, this assumption weaves the very fabric of their financial [worldview](http://en.wikipedia.org/wiki/World_view).

Much of investing and trading similarly bow to this assumption, ranging from the premise of [fundamental analysis](http://en.wikipedia.org/wiki/Fundamental_analysis) to many [modern hedge fund strategies](http://en.wikipedia.org/wiki/Hedge_fund#Strategies) (from event-driven to global macro and merger arbitrage).

*What if this assumption is wrong*? Many facts are beginning to beg this question.

While fundamentals will always move financial markets, increasingly markets themselves are driving causality and doing so at increasingly faster pace. Causality is driving both knock-on effects within the markets and corresponding fundamental changes. In other words, *financial markets are impacting the “real world”, just as much as events in the “real world” impact financial markets*.

This evolution in causality is fundamentally empowering quantitative trading.

The technical reason is the notion of exogeny is undergoing revolution. In short, *what was considered exogenous yesterday, will be endogenous tomorrow*. This will redefine the financial landscape from statistical analysis to monetary policy. For example, consider [variance decomposition](http://en.wikipedia.org/wiki/Variance_decomposition), which essentially measures informational impact of exogeneous shocks in [vector autoregressive](http://en.wikipedia.org/wiki/Vector_autoregression) (VAR) models. Similarly, consider the [IMF Exogeneous Shock Facility](http://www.imf.org/external/np/exr/facts/esf.htm) (who knew that existed!). Both will need rethinking.

Consider the following examples which make this case, and decide for yourself.

*   Credit: the current financial crisis is due, in large part, to leveraged credit instruments and their corresponding negative financial impact on both banking institutions and sovereigns; at least in part, these effects were partial knock-ons from interest rates held low to recover from the tech bubble
*   Foreign Exchange: Brunnermeier, in a recent paper [Carry Trades and Currency Crashes](http://www.princeton.edu/~markus/research/papers/carry_trades_currency_crashes.pdf), proves relationship between carry trade and currency crashes, concluding:

    > “Macroeconomic fundamentals determine which currencies have high and low interest rates and the long‐run currency levels, while illiquidity and capital immobility lead to short‐run currency underreaction to changes in fundamentals and occasional currency crashes due to liquidity crises.”

*   Volatility: VIX, which is a measure of SPX volatility and vol skew, is now consistently correlated with turmoil in “real world” fundamentals (*e.g.* VIX correctly predicted Bear Sterns bankrupcy), is regularly promoted to investors as their [fear gauge](http://www.cboe.com/micro/vix/faq.aspx#2), and is correlated with currency crashes (ibid Brunnermeier):

    > “Currency crashes are positively correlated with increases in implied stock market volatility VIX and the TED spread, indicators of funding illiquidity, among other things.”

*   High Frequency: nearly all [market microstructure](http://en.wikipedia.org/wiki/Market_microstructure), excluding event-driven, assume the evolution of security prices is modeled via convolution or filtering of past trades and the order book (see Hasbrouck [2007]), thus reducing price discovery causality solely to evolution of the market itself

Native manifest of causality in financial markets will revolutionize quantitative trading: careful quantitative analysis of markets will increasingly permit forecasting of subsequent changes in both the market itself and “real world” fundamentals. Increasingly, all factors become endogenous for quantitative models.

The open question for readers is how to build and profit from models which detect and subsequently forecast both first- and second-order causality and their corresponding knock-on effects, across both the “real world” and financial markets. [Market regimes](https://quantivity.wordpress.com/2009/12/31/market-regime-trading-redux/) seek to form part of the answer to this question, but much of the hard quantitative analysis and modeling effort remains wide open.