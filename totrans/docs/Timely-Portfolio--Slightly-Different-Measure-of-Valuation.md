<!--yml
category: 未分类
date: 2024-05-18 15:01:48
-->

# Timely Portfolio: Slightly Different Measure of Valuation

> 来源：[http://timelyportfolio.blogspot.com/2013/01/slightly-different-measure-of-valuation.html#0001-01-01](http://timelyportfolio.blogspot.com/2013/01/slightly-different-measure-of-valuation.html#0001-01-01)

I grow tired of the tried and true standard measures of valuation, and from time to time I try to think of alternate methods.  One thought was to analyze [Ken French’s Market(ME) to Book(BE) Breakpoints by percentile](http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/Data_Library/det_me_breakpoints.html).  We can see by year at what level is a stock considered cheap relative to the universe.  As these breakpoints move higher, the market is willing to pay a higher price.  In reverse, as these breakpoints move lower, stocks fetch a lower price or can be considered cheaper.  Since there are 20 fifth percentiles, a horizon plot can provide a good overall look at this measure of valuation.

Here is a horizon plot of absolute ME/BE valuation by fifth percentile since 1926.

For a more representative look, let's plot a horizon chart of the ME-BE / historical mean - 1.

For one more non-horizon look, we can use an xyplot.

In theory, I think this could provide yet another gauge of the cheapness of stocks, but of course, there is lots of research to be done.

[R Code from Gist:](https://gist.github.com/4550147)