<!--yml
category: 未分类
date: 2024-05-18 13:44:19
-->

# Volume Clock, Gaps, and GOOG | Quantivity

> 来源：[https://quantivity.wordpress.com/2012/10/23/volume-clock-gaps-and-goog/#0001-01-01](https://quantivity.wordpress.com/2012/10/23/volume-clock-gaps-and-goog/#0001-01-01)

GOOG unexpectedly disclosed their Q3 earnings early last week, on October 18th. While earnings were marginally interesting, much more amusing was the corresponding hiccup in intraday trading. This event provides an opportunity to dig into TAQ data, view through a HFT lens, and build intuition from some elegant ideas due to Mendelbrot, Clark, and Ané.

Begin by taking a look at the time-series plot of intraday trade prices for GOOG from the 18th (from one exchange):

[![](img/da5106d47760f214cf5cd0d3159c06ff.png "goog-trades-20121018")](https://quantivity.wordpress.com/wp-content/uploads/2012/10/goog-trades-20121018.png)

The tape clearly illustrates some unhappy traders, with what appears to be a gap down in the noon hour (followed by trading halt until 3pm). Intraday dynamics can be better understood with a time-series summary of the corresponding trades and quotes:

[![](img/314aa1c402f89d7ff1d32bbf8e1aee60.png "goog-taq-20121018")](https://quantivity.wordpress.com/wp-content/uploads/2012/10/goog-taq-20121018.png)

Although the price appears to gap when viewed on a low-frequency daily chart, drilling into the noon hour illustrates the contrary:

[![](img/dfa324ae99dc9fbd0cc41be5da1aa643.png "goog-taq-20121018-noon-one")](https://quantivity.wordpress.com/wp-content/uploads/2012/10/goog-taq-20121018-noon-one.png)

Rather than a single print gap, the price action evolved more slowly over 12:30 to 12:40\. The spread quickly expanded after 12:30, presumably driven by the jump in volume subsequent to disclosure. A 5,000 share trade printed shortly after 12:32, as spreads were beginning to stabilize. This precipitated some fear and greed, as market makers blew the spreads out to $4\. Spread dynamics after noon appear to be fairly typical response to uncertainty and toxicity, as the summary is qualitatively similar to other similar events such as the morning after Bear in 2008.

By way of comparison, below is plot for TAQ summary on 3:25 – 4pm:

[![](img/2ddca222ce0849df4689ac8a1ed1d24d.png "goog-taq-20121018-three-four")](https://quantivity.wordpress.com/wp-content/uploads/2012/10/goog-taq-20121018-three-four.png)

Now that we are familiar with the TAQ action as measured in human chronology, let’s view it through a different lens—following the intuition from Mandelbrot (1963), Clark (1971), and most recently Easley *et al.* (2012).

To do so, begin by considering trades for GOOG from another day which is more normal, say the following day Oct 19\. Start with human chronology, and calculate the time series of first differences for 1 and 5 minute bars. Next estimate the [Epanechnikov kernel density](http://en.wikipedia.org/wiki/Kernel_density_estimation) from first differences. Finally, fit the corresponding Gaussian for the same first differences. Or, in R:

```

# first differences
min1Diff <- diff(to.minutes(trades$price)[,4], na.pad=F)
min10Diff <- diff(to.minutes5(trades$price)[,4], na.pad=F)

# kernel densities
min1Density <- density(min1Diff, kernel="epanechnikov")
min10Density <- density(min10Diff, kernel="epanechnikov")

# corresponding normals
min1Normal <- fitdistr(coredata(min1Diff), "normal")$estimate
min10Normal <- fitdistr(coredata(min10Diff), "normal")$estimate

```

Which are plotted below for Oct 19, with solid red being 1-minute difference density and solid blue being 5-minute difference bars (ignore black for now); Gaussian fits for the same differences of each are dashed:

[![](img/111747c70c55f2747e68c58925e9c226.png "goog-clock-20121019")](https://quantivity.wordpress.com/wp-content/uploads/2012/10/goog-clock-20121019.png)

This reproduces the familiar stylized distribution of high-frequency returns, consistent with Figure 1 from Clark (1971) and Exhibit 2 from Easley *et al.* (2012). Although certainly leptokurtic, the distributions are not too dissimilar from normal.

Now, ignore chronological time and instead consider the trades from the perspective of a *clock based on volume of shares traded over the day*. In other words, generate a new process defined as the sequence of prices coinciding with shares traded on equal-sized partitions of total volume over the day. This process generates a “volume clock” for the trades, in doing so exemplifying a beautiful time-series transformation.

A similar kernel density can be estimated from this trade volume clock, which is plotted above in black (with dashed corresponding normal fit), assuming partition size of 50\. This exhibits distribution characteristics consistent with Exhibit 2 from Easley *et al.* (2012).

With intuition on volume clock densities, we can finally take a look at Oct 18 through the lens of a computer via the following plot:

[![](img/a0b2e08784b4b6478c4bf8bf1742f927.png "goog-clock-20121018")](https://quantivity.wordpress.com/wp-content/uploads/2012/10/goog-clock-20121018.png)

Needless to say, this plot for Oct 18 looks nothing like the previous plot for Oct 19\. The normal fits for both 5-min bars (blue) and volume clock (black) are especially interesting, as they have little resemblance to their corresponding kernel estimates. Care is required for trading on days that look like this.

For those interested to learn more, see Clark (1971) for theory, including subordinated stochastic processes (originally due to Bochner (1960)). Ané and Geman (2000) apply a bit more sophistication, including arguing in favor of cumulative transaction count rather than cumulative traded volume. Perhaps worth a follow-up post to see if this still makes sense, given current era of predominantly algorithmic program trading.

The R code to generate the above plots is:

```

plot(trades20121018$price, main="GOOG Trades (2012-10-18)")
plotTAQSummary("GOOG", "2012-10-18", as.POSIXct("2012-10-18 09:30:00"), as.POSIXct("2012-10-18 16:05:00"))
plotTAQSummary("GOOG", "2012-10-18 | 12:00 - 13:00", as.POSIXct("2012-10-18 12:00:00"), as.POSIXct("2012-10-18 13:00:00"))
plotTAQSummary("GOOG", "2012-10-18 | 15:00 - 16:00", as.POSIXct("2012-10-18 15:25:00"), as.POSIXct("2012-10-18 16:05:00"))
plotTimeChangeDensity("GOOG", as.Date("2012-10-19"), trades20121019)
plotTimeChangeDensity("GOOG", as.Date("2012-10-18"), trades20121018)

```

And, a bit of literature on subordinated processes, volume clocks, and price processes:

*   Bochner, Harmonic Analysis and the Theory of Probability, University of California Press, Berkeley, 1960.
*   Mandelbrot, “The Variation of Certain Speculative Prices”, Journal of Business, Vol. 36 (1963), p. 394-419.
*   Clark, “A Subordinated Stochastic Process Model with Finite Variance for Speculative Prices”. Center for Economic Research. University of Minnesota, 1971.
*   Ané and Geman, “Order Flow, Transaction Clock, and Normality of Asset Returns”, Journal of Finance, Vol. 55, No. 5 (2000), pp. 2259-2284.
*   Murphy and Izzeldin, “Order Flow, Transaction Clock, and Normality of Asset Returns: Ané and Geman (2000) Revisited”, 2006.
*   Easley, de Prado, and O’Hara, “The Volume Clock: Insights into the High Frequency Paradigm”. Journal of Portfolio Management, May 2012.