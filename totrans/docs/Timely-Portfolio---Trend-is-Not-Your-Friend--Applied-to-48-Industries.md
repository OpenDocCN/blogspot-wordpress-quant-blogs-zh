<!--yml
category: 未分类
date: 2024-05-18 15:04:27
-->

# Timely Portfolio: “Trend is Not Your Friend” Applied to 48 Industries

> 来源：[http://timelyportfolio.blogspot.com/2012/08/trend-is-not-your-friend-applied-to-48.html#0001-01-01](http://timelyportfolio.blogspot.com/2012/08/trend-is-not-your-friend-applied-to-48.html#0001-01-01)

*Please see previous post [Crazy RUT in Academic Context Why Trend is Not Your Friend](http://timelyportfolio.blogspot.com/2012/06/crazy-rut-in-academic-context.html).*

I’ll repeat the intro to the post mentioned above, so we can all get caught back up.

In response to [Where are the Fat Tails?](http://timelyportfolio.blogspot.com/2012/06/where-are-fat-tails.html), reader vonjd very helpfully referred me to this paper [The Trend is Not Your Friend! Why Empirical Timing Success is Determined by the Underlying’s Price Characteristics and Market Efficiency is Irrelevant](http://www.frankfurt-school.de/clicnetclm/fileDownload.do?goid=000000311260AB4) by Peter Scholz and Ursula Walther. The authors conclude

> “Our study on the basis of real data clearly confirms the hypothesis that the asset price characteristics of the underlying price process have a crucial impact on timing results. This allows us to forecast the timing success depending on the market's parameters. An OLS
> regression analysis supports our predictions and verifies our assumption that the drift has the
> strongest influence on timing success. By contrast, the higher moments (skewness, kurtosis)
> seem not to have any significant impact on the timing result in the empirical sample. As we
> presumed, the level of market development, and hence the degree of efficiency, does not play
> any role. Trading worked coincidentally rather well in the developed world and quite poorly in
> the emerging markets. The driving factor for the timing success is the parametric environment the trading system stumbles on…
> 
> Our study contributes to the discussion by providing a structured analysis of the relevance of the most important price process parameters. As a result, the traditional explanations for timing success can be abandoned: we find that it is very likely for the SMA trading rule to generate excess returns over its benchmark if the underlying price path exhibits negative drifts, high serial autocorrelation, low volatilities of returns, and highly clustered volatilities. Drift and autocorrelation of the underlying asset seem to have the largest impact, though.”

One of my initial ideas for extending the research was to incorporate a much larger set of indexes over a longer period of time.  As I was working on [48 Industries Since 1963](http://timelyportfolio.blogspot.com/2012/08/48-industries-since-1963.html), I decided 50 years of data on 48 different indexes would be a great dataset to apply the ideas and methods presented in the paper.

Using R and all its wonderful packages, it is surprisingly easy to accomplish.  Let’s see if we can test “drift and autocorrelation…have the largest impact” on excess returns with industries also.  I’ll try not to get too statistical.

In terms of drift or annualized return, we can see a linear inverse relationship between return and out(under)performance of the 200 day moving average system, so the better the performance of the industry, the less likely a moving average system is to outperform.

In terms of the GARCH model effects on excess returns, a parallel coordinate chart will best start our exploration.  Lines are colored by the excess return of a moving average system on each industry.

Mu and alpha1 seem to most heavily influence the ability of a moving average system to outperform.  Let’s isolate our chart to mu and alpha1 and add ar1 based on the authors’ findings.  I am very tempted to try to explain GARCH here, but for the sake of brevity, I’ll refrain.  This [paper](http://scholar.google.com/scholar?cluster=1570505569310094643&hl=en&as_sdt=0,1) and this [Portfolio Probe post](http://www.portfolioprobe.com/2012/07/06/a-practical-introduction-to-garch-modeling/) offer a good introduction to GARCH.

Now let’s look at a scatterplot of excess return versus each of the GARCH stats, starting with those with the most influence.

In conclusion, it seems the same effects observed by the authors also apply to US industry indexes.  In future posts, I’ll add a little more statistical rigor to the analysis and apply to other indexes.

Now, I just cannot resist using a horizon plot to evaluate the rolling 250 day excess returns of a moving average system over buy and hold.  As you can see, a bull market favors buy and hold.  The 70s and 2008-2009 were very kind to a moving average approach.

[R code in GIST (do raw for copy/paste):](https://gist.github.com/3298278)