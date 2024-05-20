<!--yml
category: 未分类
date: 2024-05-18 13:51:58
-->

# Higher Moments and Minimum Variance | Quantivity

> 来源：[https://quantivity.wordpress.com/2011/04/30/higher-moments-minimum-variance-portfolios/#0001-01-01](https://quantivity.wordpress.com/2011/04/30/higher-moments-minimum-variance-portfolios/#0001-01-01)

Several subsequent posts will analyze the relevance and comparative performance of higher and mixed [moments](http://en.wikipedia.org/wiki/Moment_(mathematics)) to [minimum variance portfolios](https://quantivity.wordpress.com/2011/04/17/minimum-variance-portfolios/) (along with [CVaR / ES](http://en.wikipedia.org/wiki/Expected_shortfall) and [lower partial moments](http://en.wikipedia.org/wiki/Moment_(mathematics)#Partial_moments)), extending previous [US sector](https://quantivity.wordpress.com/2011/04/22/minimum-variance-sector-rotation-part-2/) and [global rotation](https://quantivity.wordpress.com/2011/04/24/minimum-variance-global-rotation/) models. To help motivate this, consider the following quote from [Amaya and Vasquez](http://www.efmaefm.org/0EFMAMEETINGS/EFMA%20ANNUAL%20MEETINGS/2010-Aarhus/EFMA2010_0137_fullpaper.pdf) [2010], which conjectures that *compensation for volatility depends on skewness level* (p. 16):

> Stocks with negative skewness are compensated as suggested by the mean-volatility model: more volatility translates into more returns. However, as skewness increases and becomes positive, the positive relation between volatility and returns turns into a negative relation. For stocks with positive skewness, higher volatility means lower returns. Even more, the lowest returns are earned by the portfolio with stocks that have high positive skewness and high volatility.

This is an interesting extension of minimum variance, nuancing the role of volatility consistent with previously conjectured lottery-seeking investor behavior and thus further affirmation of [portfolio theory being dead](https://quantivity.wordpress.com/2011/04/10/portfolio-theory-is-dead-now-what/) (ibid):

> Stocks with low skewness are compensated with high returns when volatility increases, but stocks with high skewness are compensated with high returns when volatility decreases. This compensation for volatility presents somewhat of a puzzle given that, under the mean-variance model, investors always prefer low volatility and not high volatility as implied by our result. Hence, we argue that investors accept low returns and high volatility only because they are more attracted to high positive skewness; they are skewness lovers or lotto investors.

Although this return-variance-skew relationship is intuitively obvious to traders, this article nicely extends the intuition motivating minimum variance optimization into higher moments.