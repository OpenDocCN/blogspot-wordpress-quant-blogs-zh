<!--yml
category: 未分类
date: 2024-05-12 18:25:20
-->

# Percentrank SMA | CSSA

> 来源：[https://cssanalytics.wordpress.com/2010/05/19/percentrank-sma/#0001-01-01](https://cssanalytics.wordpress.com/2010/05/19/percentrank-sma/#0001-01-01)

*Some good recent links worthwile reading:*

Rob Hanna at Quantifiable Edges looks at intraday behavior: [#mce_temp_url#](http://quantifiableedges.blogspot.com/2010/05/from-1-up-intraday-to-1-down-close.html)

Dave at MindMoneyMarkets looks at an often overlooked detail–the performance of indicators on index prices versus actual traded ETFs: [http://davesbrain.blogs.com/mindmoneymarkets/](http://davesbrain.blogs.com/mindmoneymarkets/)

Michael at MarketSci looks at different variations of the Golden Cross: [http://marketsci.wordpress.com/2010/05/18/the-golden-cross-daily-vs-weekly-vs-monthly/](http://marketsci.wordpress.com/2010/05/18/the-golden-cross-daily-vs-weekly-vs-monthly/)

Quantum Financier (a new but very promising new blog) looks at using the Probability Density Function to create an adaptive RSI: [http://quantumfinancier.wordpress.com/2010/05/14/using-probability-density-as-an-adaptive-mechanism/](http://quantumfinancier.wordpress.com/2010/05/14/using-probability-density-as-an-adaptive-mechanism/)

Engineering Returns (a new but very promising new blog) takes an interesting look on filtering for inside bars in a mean-reversion strategy: [http://engineering-returns.com/2010/05/18/spy-a-quantitative-view-at-inside-bars/](http://engineering-returns.com/2010/05/18/spy-a-quantitative-view-at-inside-bars/)

This is a  simple twist on using the now infamous “percentrank” function to create a trend following metric. The advantage of the percentrank SMA (P-SMA) is that it is continuous and captures the distribution of a price series versus just a binary signal. It is also more stable than a percentrank of price.  The calculation metric I used in this post is as follows:  **P-SMA= percentrank(sma(n),250)**You can choose the moving average length of your choice, but due to the nature of the calculation I suggest using values equal to or under 50 to be commensurate in duration with say the golden cross or 200sma. The general idea is to avoid looking at the price which tends to be volatile and noisy, and instead look at the average/midpoint of the price series and normalize its movement over time. In this case, unlike other indicators that use the percentrank, we are not neccessarily looking exclusively at above/below the median since we are already using the average which is more stable than price. The lag introduced by a long moving average versus a relatively short distribution measurement (250) requires that we potentially lower our threshold for what would constitute an uptrend.

In this case I looked at how the 50 day P-SMA performs on the S&P500 index over the last 12,000 bars at various thresholds going long and short versus the Golden Cross as a basis of comparison. Results are presented below showing the CAGR and the cumulative return of $1 since inception. Note that performance on the SPY over the last 2000 bars was 10% CAGR for the .5 threshold which shows that the indicator performs well also in the recent past on a tradeable instrument versus  the index.

On balance the percentrank SMA at the 50 parameter performs better than the Golden Cross, and shorter variations while not shown tend to perform quite well in relation to comparable moving averages or crossovers. In my opinion, the selling point isn’t really the outperformance (which is nice) but rather that you can do so much more at a systems creation level with a continuous trend indicator than a crossover. Possible applications involve percentage exposure models, or even more interesting would be to use the indicator values to adjust shorter term indicator values/signals.

Percentrank SMA Various  Entry Thresholds Versus Golden Cross (12000 bars)

Golden Cross >.5 >.45 >.4 >.35 CAGR 6.13% 6.18% 6.45% 7.44% 6.84% Cumulative Product 17.40 17.74 20.071 31.27 23.97 Factor