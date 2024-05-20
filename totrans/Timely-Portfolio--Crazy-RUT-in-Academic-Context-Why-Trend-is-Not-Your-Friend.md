<!--yml
category: 未分类
date: 2024-05-18 15:05:54
-->

# Timely Portfolio: Crazy RUT in Academic Context Why Trend is Not Your Friend

> 来源：[http://timelyportfolio.blogspot.com/2012/06/crazy-rut-in-academic-context.html#0001-01-01](http://timelyportfolio.blogspot.com/2012/06/crazy-rut-in-academic-context.html#0001-01-01)

In response to [Where are the Fat Tails?](http://timelyportfolio.blogspot.com/2012/06/where-are-fat-tails.html), reader vonjd very helpfully referred me to this paper [The Trend is Not Your Friend! Why Empirical Timing Success is Determined by the Underlying’s Price Characteristics and Market Efficiency is Irrelevant](http://www.frankfurt-school.de/clicnetclm/fileDownload.do?goid=000000311260AB4) by Peter Scholz and Ursula Walther.  The authors conclude

> “Our study on the basis of real data clearly confirms the hypothesis that the asset price characteristics of the underlying price process have a crucial impact on timing results. This allows us to forecast the timing success depending on the market's parameters. An OLS
> regression analysis supports our predictions and verifies our assumption that the drift has the
> strongest influence on timing success. By contrast, the higher moments (skewness, kurtosis)
> seem not to have any significant impact on the timing result in the empirical sample. As we
> presumed, the level of market development, and hence the degree of efficiency, does not play
> any role. Trading worked coincidentally rather well in the developed world and quite poorly in
> the emerging markets. The driving factor for the timing success is the parametric environment the trading system stumbles on…
> 
> Our study contributes to the discussion by providing a structured analysis of the relevance of the most important price process parameters. As a result, the traditional explanations for timing success can be abandoned: we find that it is very likely for the SMA trading rule to generate excess returns over its benchmark if the underlying price path exhibits negative drifts, high serial autocorrelation, low volatilities of returns, and highly clustered volatilities. Drift and autocorrelation of the underlying asset seem to have the largest impact, though.”

They go a long way toward answering my puzzle “Why has the Russell 2000 been so difficult to beat over the last decade?”  I have made a lot of progress in replicating their research in R, but for now, let’s have a messy look at their **Table 2: Descriptive statistics of 35 leading equity indices** with ggplot2.

Now let’s combine **Table 2** with their **Table 21: Average excess return from timing in the 35 selected leading equity indices**with a little graphical help from R.  The colors in the chart indicate the sum of all outperformance by the multiple moving averages.  Red, such as China and Russia, demonstrates drastic underperformance of the moving average strategies versus buy and hold.  If excess return was symmetrical, we would expect bright green similar to the bright red, but instead we only see dull gray in the bottom left indicating slight outperformance.

Now that we have established the context, we will explore in future posts where the Russell 2000 fits in terms of statistical properties and see if the this fits the authors discoveries.

Thanks again to reader vonjd for leading me to this fine work by Peter Scholz and Ursula Walther.

[R code from GIST (choose raw for copy/paste):](https://gist.github.com/2996948)