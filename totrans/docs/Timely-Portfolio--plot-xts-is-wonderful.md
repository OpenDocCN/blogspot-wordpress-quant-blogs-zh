<!--yml
category: 未分类
date: 2024-05-18 15:04:15
-->

# Timely Portfolio: plot.xts is wonderful

> 来源：[http://timelyportfolio.blogspot.com/2012/08/plotxts-is-wonderful.html#0001-01-01](http://timelyportfolio.blogspot.com/2012/08/plotxts-is-wonderful.html#0001-01-01)

As mentioned in FOSS Trading post [A New plot.xts](http://blog.fosstrading.com/2012/08/a-new-plot-xts.html) yesterday

> “The [Google Summer of Code (2012)](http://google-melange.appspot.com/gsoc/homepage/google/gsoc2012) project to [extend xts](http://rwiki.sciviews.org/doku.php?id=developers:projects:gsoc2012:xts) has produced a very promising new plot.xts function. Michael Weylandt, the project's student, wrote [R-SIG-Finance](https://stat.ethz.ch/mailman/listinfo/r-sig-finance) to [request impressions, feedback, and bug reports](http://draft.blogger.com/%20https://stat.ethz.ch/pipermail/r-sig-finance/2012q3/010652.html). The function is housed in the [xtsExtra](https://r-forge.r-project.org/scm/viewvc.php/pkg/xtsExtra/?root=xts) package of the [xts project on R-Forge](https://r-forge.r-project.org/projects/xts).
> 
> Please try xtsExtra::plot.xts and let us know what you think. A sample of the eye-candy produced by the code in [Michael's email](https://stat.ethz.ch/pipermail/r-sig-finance/2012q3/010652.html) is below. Granted, this isn't a one-liner, but it's certainly impressive! Great work Michael!”

and as announced by author Michael Weylandt in [https://stat.ethz.ch/pipermail/r-sig-finance/2012q3/010652.html](https://stat.ethz.ch/pipermail/r-sig-finance/2012q3/010652.html "https://stat.ethz.ch/pipermail/r-sig-finance/2012q3/010652.html")

> “As the community which makes the most heavy use of xts, I would like to draw your attention to a new set of plotting functions for xts objects available as part of Google Summer of Code 2012\. This work represents a major overhaul of previously existing plot.xts and should provide you with the most comprehensive and flexible time series plotting available in R. Features include:
> 
> *   "automagic" layout construction and axis alignment
> *   smart argument recycling
> *   panel function abilities
> *   more attractive candle and bar plots for OHLC objects
> *   scatterplots to view the co-evolution of multiple series
> *   event markers
> *   regime highlighting
> *   time-oriented barplots via barplot.xts [based on code by Peter Carl]
> *   interoperability with all known R time series classes using the xts try/reclass paradigm
> 
> while retaining the same smart axis formatting and gridlines that plot.xts provided. We have made every effort to maintain complete compatibility with documented usages of the old plot.xts and to be 95% compatible with plot.zoo. My goal has been to craft a design which uses smart defaults to put attractive and informative graphics ever at your fingertips, while remaining flexible enough for "power-users" to craft every detail as they desire…”

Michael has done a fantastic job with this Google Summer of Code (GSOC) project, and I look forward to incorporating all the new features of plot.xts.  As a quick example very different from that shown in the post and mailing list announcement, I thought it would be fun to show how we can use plot.xts to replace the veteran chart.TimeSeries and charts.PerformanceSummary plots from the PerformanceAnalytics package.

For the chart.TimeSeries, I will almost exactly replicate the chart given in the documentation.

Not really as a useful application but for the sake of demonstration, we can produce something like this to separate styles and also avoid event label collision (just implemented by Michael very late last night).

plot.xts even allows plot.zoo and lattice panel type functionality which allows us to do very nice things like in this charts.PerformanceSummary style chart.

I very much appreciate this very powerful contribution to R.  Thanks to everyone involved.

[R code in GIST (note: install xtsExtra from R-forge)](https://gist.github.com/3373828) :