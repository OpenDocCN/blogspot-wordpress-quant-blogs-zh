<!--yml
category: 未分类
date: 2024-05-18 14:02:54
-->

# Improved Key Perfomance Statistics – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2010/09/10/improved-key-perfomance-statistics/#0001-01-01](https://quantumfinancier.wordpress.com/2010/09/10/improved-key-perfomance-statistics/#0001-01-01)

With the goal to improve reader experience on the blog, I will be introducing a new performance statistics report for backtest results. In deciding what I would be using, I used reader feedback and I went on other blogs I follow to see what they were using. This way I think readers will be able to easily compare the different ideas they see across the blogosphere. As a guideline, I will from now on be using a statistical output relatively similar to the output produced by the [DVixl platform](http://dvindicators.cssanalytics.com/product/dvix/) (highly recommended product). In addition, I am going to be inserting three other measures in the tables. They are described below.

**Sortino Ratio**

This ratio is a measure of the risk-adjusted return of the strategy. It is, in my opinion an improved version of the popular Sharpe ratio. The Sharpe ratio is computed using the mean return divided by the standard deviation of returns. While its simplicity is appealing, it isn’t a flawless measure (none is); it penalize both upside and downside volatility. From an intuitive point of view, only penalizing downside volatility make more sense, because upside volatility is desirable for investors. This is exactly what the Sortino ratio does (from wiki):

![](img/54a77f13b252bdff54b7e9c4c548d0ac.png "Sortino Ratio Formula")

Where R is the asset or portfolio realized return; T is the target or required rate of return for the investment strategy under consideration, (T was originally known as the minimum acceptable return or MAR); DR is the downside risk. Note that for the statistic on the blog, the MAR is going to be 0, same as in the Sharpe calculation.

**Historical Value-at-Risk (95%)**

For a very nice explanation of the VaR concept, see [this article](http://cssanalytics.wordpress.com/2010/02/04/introduction-to-d-var-position-sizing-part-1/) by David Varadi. The value reported will be the ex-post (after the fact) value of the 5th percentile on the negative returns empirical distribution. It indicates that historically, we had daily returns worse that the value 5% of the time. Note that this is a non-parametric VaR which I prefer to the version assuming Gaussian distribution.

I hope that the new format which will be employed in future backtests will satisfy a broader audience of reader, and I also think that it will improve the value of the blog. In a short period of time, I will be posting strategies that I consider more tradable than the concepts I have talked about before and I think that the new format will be better to convey their value.

QF