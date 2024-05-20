<!--yml
category: 未分类
date: 2024-05-12 20:34:09
-->

# Falkenblog: Do Low Vol Tactics Matter?

> 来源：[http://falkenblog.blogspot.com/2012/03/do-low-vol-tactics-matter.html#0001-01-01](http://falkenblog.blogspot.com/2012/03/do-low-vol-tactics-matter.html#0001-01-01)

An important question for any strategy is how important tactics are. That is, for some strategies, tactics are unimportant because the algorithm has a 'flat maximum', where lots of parameters generate outputs very nearly as good as the optimal parameters. Debt models have this characteristic, as a handful of inputs generate the optimal metric pretty well with a variety of weightings and transformations.

What about low volatility investing, where one can invest several ways. In the first, you take stocks with the lowest variance over the past N days, and form a portfolio. That's the route the

[SPLV](http://www.invescopowershares.com/products/overview.aspx?ticker=SPLV)

etf takes. Or you could take the stocks with the lowest beta. Then, there's the factor approach, which applies mean-variance optimization to a set of latent factors drawn from the cross-section of stocks. Standard constrained-optimization algorithms can be applied to this problem. There are other ways, such as how the

[LVOL](http://www.russelletfs.com/Products/LVOL_Index.aspx)

etf chooses stocks that closely fit a low-vol portfolio proxy, but I find that a bit too complicated.

In any case, I took 1500 non-etf US stocks, and applied the beta, volatility, and factor approach using daily data through Feb 2011, and then looked at the resulting porfolios over the next year. Each portfolio had about 100 stocks, and they overlapped by about 65 stocks. Volatility was reduced by about 45% relative to the equal-weighted benchmark that it was drawn from. In contrast, value and growth strategies had very different trajectories. This suggests the specific algorithm doesn't matter much if you are merely targeting low volatility.

[![](img/5a37b915b5ecd4356b353c7b5d112c6b.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjO2UBBfgPgpx7EK2NpMr-8D1yMvG4pgKOcXk-d2Z29GBOLfkqKVI2qXMpB30vXQ1YE7xPDIGj3cX1o4tfWjFcZqymJhJrNpi59PWouXNyW9DEHSV8xyX7SUi7oM8g4vv_rnzWs3A/s1600/totret2.png)