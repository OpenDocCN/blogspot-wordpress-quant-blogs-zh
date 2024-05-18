<!--yml
category: 未分类
date: 2024-05-18 14:01:29
-->

# Market Neutrality – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2010/11/27/market-neutrality/#0001-01-01](https://quantumfinancier.wordpress.com/2010/11/27/market-neutrality/#0001-01-01)

Market neutrality is one of those buzz words thrown around quite a lot in finance; several hedge funds claim their strategies as being market neutral and use it as their main marketing tool. Some quantitative strategies are also oriented towards that goal; pairs trading is a prime example, but one can also include segments of statistical arbitrage in that broad area.

This begs the question why market neutral? To answer this question we must first discuss what market neutrality means. Consider the daily return for a stock ![i](img/925b1f6660c334a161416f0e9fd11e99.png) denoted ![R_i](img/828705a00fc9fb273a734ee3c24b4a2d.png). We can decompose the returns between the market related (systematic) portion ![F](img/00ff0125f3f48705d02671ac754bf484.png) and the stock specific (idiosyncratic) portion ![\Theta](img/5275ad89f099ecf59490ce4c0d08f371.png), yielding the following equation:

![R_i = \beta_i F + \Theta_i](img/2dae825c921cb86639c4b54749bd8503.png)

Which is nothing more than an ordinary least squares regression model decomposing the return of stock ![i](img/925b1f6660c334a161416f0e9fd11e99.png) into a systematic component ![\beta_i F](img/ee0e11c39ff8c67091b959f9271a1ff0.png) and an idiosyncratic (uncorrelated) component ![\Theta_i](img/cad8b0798d4b651ad4225fcba505f65f.png). The market neutrality is obtained by eliminating the systematic portion of the returns, equivalent to say:

![\beta_i F = 0](img/1aa808fca967d8fe6b21abbdd1fd255d.png)

Implying:

![R_i = \Theta_i](img/e1a53fb4bd946baaeacce9bd5e1bea39.png)

Effectively, getting rid of the market exposure and only exposing ourselves to the portion of the return based on stock ![i](img/925b1f6660c334a161416f0e9fd11e99.png) specific profile, hence market neutrality. Now back to the initial question: why market neutral? Simply put; we want to make a bet on a security without at the same time betting on the direction of the market. In a relative value strategy like pairs trading where we are betting on the outperformance of securities relative to each other, regardless of where the market goes, market neutrality takes all its sense.

However market neutrality is not only considered in relative value strategies. Imagine an investor trading a portfolio of strategies. The market exposure of this particular investor can be thought as the capital weighted average of the individual strategy betas:

![\beta_p = \frac {Q_j}{\sum Q_j} \beta_j](img/3030768b18f2a46ca85f3227208dba15.png)

Where ![Q_j](img/3a67eed332abf1957da8075fba8f4e4c.png) is the dollar amount invested in strategy ![j](img/062bd45c0d8384d16086c0cdd1d87867.png).

Keeping in mind the first equation we can also decompose the return of the portfolio in a similar fashion, composed of a systematic and idiosyncratic (strategy ensemble specific) component. In an attempt to obtain market neutrality, one could short (buy) market futures or the corresponding ETF in order to satisfy the second equation, effectively neutralizing the portfolio returns’ exposure to the market.

While this approach does not necessarily improve returns, it has the benefit of potentially better sheltering one against market storms by reducing exposure. Targeting a market neutral approach also has the benefit producing uncorrelated returns. A recent post by [Marketsci](http://marketsci.wordpress.com/2010/09/07/investors-don%E2%80%99t-really-want-absolute-returns/) explain that most investors don’t seem to look for absolute returns, but if you find yourselves in the category that would prefer absolute to relative returns, taking a look at market neutrality may be worth your time. I personally like market neutral strategies and if interest warrants, I could dive deeper into different techniques to obtain market neutrality that I find more reliable than ordinary least squares, like quantile regression.

QF