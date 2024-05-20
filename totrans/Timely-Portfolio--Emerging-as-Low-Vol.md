<!--yml
category: 未分类
date: 2024-05-18 15:03:12
-->

# Timely Portfolio: Emerging as Low Vol

> 来源：[http://timelyportfolio.blogspot.com/2012/10/emerging-as-low-vol.html#0001-01-01](http://timelyportfolio.blogspot.com/2012/10/emerging-as-low-vol.html#0001-01-01)

Extending the series begun with [When Russell 2000 is Low Vol](http://timelyportfolio.blogspot.com/2012/10/when-russell-2000-is-low-vol.html), I thought I should take a look at Emerging Market stocks during periods of low relative volatility to the S&P 500.  So you can replicate even without access to expensive data, let’s use the Vanguard Emerging Market Fund (VEIEX) and the Vanguard S&P 500 Fund (VFINX) as proxies.  In the 12 month rolling regression, we see the same fairly steadily increasing beta and correlation of the Emerging Market stocks to the S&P 500 that we saw in the Russell 2000.

If I progress further on this research, I will have to work on an adaptive definition of “low vol”, but for the purpose of this post, I defined “low vol” as

> Emerging 50 day std. dev – S&P 500 50 day sd > –0.075

For the Russell 2000, we used a more strict 0.0125.  Although the numeric definition is different, the chart shows a very similar profile.

[R code from GIST:](https://gist.github.com/3823445)