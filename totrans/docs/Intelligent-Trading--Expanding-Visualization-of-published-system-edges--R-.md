<!--yml
category: 未分类
date: 2024-05-18 04:44:17
-->

# Intelligent Trading: Expanding Visualization of published system edges (R)

> 来源：[http://intelligenttradingtech.blogspot.com/2012/02/expanding-visualization-of-published.html#0001-01-01](http://intelligenttradingtech.blogspot.com/2012/02/expanding-visualization-of-published.html#0001-01-01)

I happened to be looking over a revised text of a systems author I happen to follow. I will be a bit vague about specifics, as the system itself is based on well known ideas, but I'll leave the reader to research related systems.  The basic message illustrated in this post, is that I often make an effort to look at different viewpoints of system related features that are not always explored in the texts.

Fig 1\. BarGraph Illustration showing 0.48% average weekly gain given conditional system parameters,  over arbitrary trades giving 0.2% average return per week over same 14 yr. period.

For example, the following system is based upon buying at pullbacks of a certain equity series and holding for a week.  In the book, a bargraph is shown illustrating the useful edge of about 0.48%/trade vs. simply buying and holding for 0.2%/trade.  Although, the edge is useful and demonstrated well in the bargraph illustration, it can be useful to look at the system performance from various different perspectives.

As an example, we might wonder how the system unfolded over time.  In order to look at this, we can plot a time series representation of the system's equity curve (assuming 100% compounding, no slippage, and no fractional sizing).  The curve is shown compared to a straw-broom plot of 100 monte carlo simulation paths of the true underlying data, comprised of randomly and uniformly selected data over the same period.

Figure 2\. Plot of edge based equity path vs. simulated Monte Carlo Straw-Broom Plots of randomly selected series based upon true underlying data.

Looking at the 'unwinding' of the actual system's 14yr. time series path, we can make a few observations.

1) The edge, in terms of terminal wealth only, far outperforms several randomly simulated data paths built from the actual instrument.

2) Unfortunately, the edge also has very wild swings and variation (resulting in a very large drawdown).

Had we blindly selected the system itself based upon the bar graph alone, it's very possible, that we could have entered at the worst possible time (just prior to the drawdown).  It also illustrates an issue I personally have with using simple monte carlo analysis (with IID assumptions) as a proxy to underlying data. Namely, that the auto-correlation properties have been filtered out, making the system based edge appear much better in comparison.  I have spent a lot of time thinking about ways to deal with this issue; but it's a discussion for another day.  But it's not necessarily a bad result at all. Rather it gives us some features (persistence and superior edge/trade) that we can use as a spring-board for further optimization; for example, we might think about adding a conditional filter to mitigate the large drawdown based upon underlying features that may have coincided during that period.

Data was plotted using R ggplot2\. Although I think the plotting tool is excellent, I find that the processing time is a bit consuming.