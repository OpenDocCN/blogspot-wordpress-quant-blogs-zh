<!--yml
category: 未分类
date: 2024-05-18 15:06:06
-->

# Timely Portfolio: Pretty Correlation Map of PIMCO Funds

> 来源：[http://timelyportfolio.blogspot.com/2012/06/pretty-correlation-map-of-pimco-funds.html#0001-01-01](http://timelyportfolio.blogspot.com/2012/06/pretty-correlation-map-of-pimco-funds.html#0001-01-01)

As [PIMCO expands beyond fixed income](http://www.pimco.com/EN/Insights/Pages/Neel%20Kashkari%20Discusses%20PIMCO%20Equity%20Platform.aspx), I thought it might be helpful to look at correlation of PIMCO mutual funds to the S&P 500.  Unfortunately due to the large number of funds, I cannot use the chart.Correlation from PerformanceAnalytics.  I think I have made a pretty correlation heatmap of PIMCO institutional share funds with inception prior to 5 years ago.  Of course this eliminates many of the new strategies, but it is easy in the code to adjust the list.  I added the Vanguard S&P 500 fund (VFINX) as a reference point.  Then, I orderded the correlation heat map by correlation to VFINX.

As expected there are two fairly distinct groups of funds: those (mostly fixed income) with negative/low correlation to the S&P 500 and those with strong positive correlation.

Here is the more standard heat map with dendrogram ordering, which has its purpose but gets a little busy.

If we are only interested in the correlation to the S&P 500 (VFINX), then this might be more helpful.

[R code from GIST:](https://gist.github.com/2931640)