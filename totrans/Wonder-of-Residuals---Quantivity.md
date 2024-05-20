<!--yml
category: 未分类
date: 2024-05-18 13:52:50
-->

# Wonder of Residuals | Quantivity

> 来源：[https://quantivity.wordpress.com/2009/08/02/wonder-of-residuals/#0001-01-01](https://quantivity.wordpress.com/2009/08/02/wonder-of-residuals/#0001-01-01)

Some mathematical [constructs](http://en.wikipedia.org/wiki/Construct_(philosophy_of_science)) appear so repeatedly across trading strategies that they evolve into [mental models](http://en.wikipedia.org/wiki/Mental_model) for quantitative trading. Each of these constructs deserve their own post, given their fundamental role in algorithmic trading.

Residuals are one of these wonderful constructs.

Many [market-neutral](http://en.wikipedia.org/wiki/Market_neutral) strategies are derived from residuals, particularly the arbitrage family: volatility arbitrage, dispersion arbitrage, index arbitrage, basket arbitrage, correlation arbitrage, *etc*. Residuals also open for trading an infinite-sized universe of investable assets, rather than just the instruments for which quotes are available from [Yahoo](http://finance.yahoo.com) or [Bloomberg](http://www.bloomberg.com).

Conceptually, a residual is deceptively simple:

> Residual is the difference between a sample and its corresponding estimated function value.

For example, the [Mean Reversion](https://quantivity.wordpress.com/2009/07/19/mean-reversion/) post estimated the following linear relationship between SPY and PRF during the 2007-2008 period:

`PRF = -7.356 + (0.455 * SPY)`

This function generates an estimated value of PRF, given a value for SPY. Translating this into trading: buy one share of PRF, short 0.455 shares of SPY, and pay $7.356 in cash. This combination forms a [basket](http://en.wikipedia.org/wiki/Basket_(finance)) (which is a generalization of the classic [pair](http://en.wikipedia.org/wiki/Pairs_trade)), which is a *synthetic instrument*. This synthetic can be bought or sold at an exchange at any time, just like any traditional asset.

Given this synthetic, first question is how is it priced? You guessed it: price of the synthetic is equal to the residual! Specifically, equal to difference between the actual price of PRF (sample) versus the value estimated by the equation. Specifically, the price of the synthetic is as follows, rearranging the function to solve for the residual term (ε):

`ε = PRF - (0.455 * SPY) + 7.356`

This innocent-looking equation belies wonder, and is worth briefly dwelling upon: a *residual prices a synthetic linear combination of assets* (SPY, PRF, and cash in this example). Similarly, the profit to hold this pair between yesterday and today is equal to subtracting value of the residual today from yesterday’s value. More generally, profit of holding the synthetic can be calculated between any two times *t* and *t+1*:

profit = ε[t+1] – ε[t]

This simple example hints at a very deep generalization, owing to basic algebra: an infinite number of linear combinations exist for two or more assets, let alone the investable universe of assets (worldwide equities, commodities, fx, and corresponding derivatives). If there are an infinite number of linear combinations, then there are an infinite number of residuals. If infinite residuals, then there are an infinite number of synthetics.

In other words, *residuals open the door for investment into an infinite number of potential assets*, rather than the mere thousands in the traditional investable universe. Pretty amazing for the little greek letter epsilon which statistics ironically refers to as the [“error”](http://en.wikipedia.org/wiki/Errors_and_residuals_in_statistics).

Synthetics are just one wonderful fruit of residuals. Subsequent *Wonder* posts will cover non-OLS residuals (*e.g.* generalized regression, state space models, and wavelets) and techniques for using residuals to choose trades amongst this infinite-sized universe of investments and evaluate their stability via techniques such as variance analysis and [structural change](http://en.wikipedia.org/wiki/Structural_change) (*e.g.* variance ratio test, [ACF](http://en.wikipedia.org/wiki/Autocorrelation), [Chow](http://en.wikipedia.org/wiki/Chow_test) / Quandt tests, and iterative coefficient estimates).