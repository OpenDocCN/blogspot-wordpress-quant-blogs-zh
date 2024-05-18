<!--yml
category: 未分类
date: 2024-05-18 15:05:06
-->

# Timely Portfolio: Application of Horizon Plots

> 来源：[http://timelyportfolio.blogspot.com/2012/07/application-of-horizon-plots.html#0001-01-01](http://timelyportfolio.blogspot.com/2012/07/application-of-horizon-plots.html#0001-01-01)

*for background please see prior posts* [*Horizon Plot Already Available*](http://timelyportfolio.blogspot.com/2012/06/horizon-plot-already-available.html) *and* [*Cubism Horizon Charts in R*](http://timelyportfolio.blogspot.com/2012/06/cubism-horizon-charts-in-r.html)

Good visualization simplifies, and stories are better told with effective and pretty visualizations.

Although horizon plots are not immediately intuitive, I have embraced them as an extremely effective method of analyzing more than four series.  I hope they become much more popular, so I can use them with much more confidence.  If we look at a traditional cumulative growth chart on the managers dataset provided by PerformanceAnalytics, I get confused by too many lines and colors since there are 10 different series.  While this chart works, it can be better.

We could panel the data, but I think this makes comparison even more difficult.

In this case and many others, horizon plots provide what I feel to be both a more attractive and effective visualization.  Here is an example using latticeExtra’s horizonplot function with very little adjustment.  You can detect both comovement or seasonality and can compare the amplitude simultaneously.

With a little additional formatting, we can get an ideal visualization-pretty and effective.  The ability to scale well beyond 10 series offers power that we cannot obtain with a traditional line chart.

As another example, let’s look at how we can use horizon plots to monitor a moving average system similar to [the Mebane Faber's timing model.](http://www.mebanefaber.com/timing-model/ "http://www.mebanefaber.com/timing-model/")  If you follow the link, you can see a decent visualization of the price and moving average.  A horizon plot could accomplish this much more efficiently.

I personally like the mirrored horizon plot even better.  Let’s incorporate that.

Please help me popularize these extremely powerful charts.

[R code from GIST (do raw for copy/paste):](https://gist.github.com/3218639)