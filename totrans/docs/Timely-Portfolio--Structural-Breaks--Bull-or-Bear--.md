<!--yml
category: 未分类
date: 2024-05-18 15:07:20
-->

# Timely Portfolio: Structural Breaks (Bull or Bear?)

> 来源：[http://timelyportfolio.blogspot.com/2012/04/structural-breaks-bull-or-bear.html#0001-01-01](http://timelyportfolio.blogspot.com/2012/04/structural-breaks-bull-or-bear.html#0001-01-01)

When I spotted the bfast R package, I could not resist attempting to apply it to identify bull and bear markets.  For all the details that I do not understand, please see the references:

> [Jan Verbesselt, Rob Hyndman, Glenn Newnham, Darius Culvenor (2010). Detecting Trend and
>   Seasonal Changes in Satellite Image Time Series. Remote Sensing of Environment, 114(1),
>   106-115\. doi:10.1016/j.rse.2009.08.014](http://scholar.google.com/scholar?cluster=4712171228077468601&hl=en&as_sdt=0,1)
> 
> [Jan Verbesselt, Rob Hyndman, Achim Zeileis, Darius Culvenor (2010). Phenological Change
>   Detection while Accounting for Abrupt and Gradual Trends in Satellite Image Time
>   Series. Remote Sensing of Environment, 114(12), 2970 - 2980.
>   doi:10.1016/j.rse.2010.08.003](http://scholar.google.com/scholar?cluster=13047717591266370513&hl=en&as_sdt=0,1)

I believe the result on the S&P 500 (even with a high h and only one iteration) is a fairly close marker for bull and bear markets, and I thoroughly enjoyed applying forestry techniques to financial time series.

[R code from GIST:](https://gist.github.com/2502879)