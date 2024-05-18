<!--yml
category: 未分类
date: 2024-05-18 13:55:13
-->

# Quote Arrival Frequency Distribution for Tick Data | Quantivity

> 来源：[https://quantivity.wordpress.com/2009/12/27/quote-arrival-frequency-distribution-for-tick-data/#0001-01-01](https://quantivity.wordpress.com/2009/12/27/quote-arrival-frequency-distribution-for-tick-data/#0001-01-01)

High-frequency systems development is built upon the analysis of tick data. A classic example is statistically characterizing the frequency and arrival times of intra-day quotes, useful for building systems which exploit [market microstructure](http://en.wikipedia.org/wiki/Market_microstructure) effects.

Yet, the temporal regularity of such analysis fundamentally differs from traditional quantitative analysis: ticks arrive at irregularly-spaced times (even multiple at the same time), with time intervals ranging from zero to a few seconds (or even minutes). The irregular time arrival of ticks conflicts with the regularly-spaced assumption of classic statistical time series methods and corresponding computational tools.

Recent analysis bore out this challenge.

Consider generating a [frequency distribution](http://en.wikipedia.org/wiki/Frequency_distribution) for quote arrival times for a single currency instrument, say EURUSD stored in a standard CSV file of the following format (with header line):

`pair,date,bid,ask
EURUSD,2009-01-26 00:00:11.000,1.294500,1.294800`

Considering all such irregularly-spaced quotes for 26 Jan 2009, calculate the temporal frequency distribution by both hour and minute. Turns out this is a bit harder in R than one naïvely expects. Any readers with R expertise, suggestions are welcome for improving the below code (admittedly not the most beautiful).

Assume a data frame, named *data*, has been loaded which contains all the above tick data. Begin by parsing the dates assuming a non-standard format, generating an ordered vector of *numeric* timestamps, measured in number of seconds since the epoch:

`datesNum <- as.numeric(as.POSIXct(strptime(as.character(data$date), "%Y-%m-%d %H:%M:%OS")))`

Next, truncate timestamps to be zero-based and convert to desired time unit (divide by 60 for minutes, 360 for hours):

`datesNum <- datesNum - min(datesNum)
datesNum <- datesNum / 60`

Now comes the R magic, made possible by converting the quote arrival timestamps into numerics:

`plot(cbind(table(cut(datesNum, seq(min(datesNum), max(datesNum), by=1), right=FALSE))), type="l", xlab="Minutes", ylab="Quote Frequency")`

This expression requires a bit of unpacking to see how it fits together (for more detailed explanation, see [r-tutor](http://www.r-tutor.com/elementary-statistics/quantitative-data/frequency-distribution-quantitative-data)):

*   Range: calculate the range of timestamps, as returned by `min()` and `max()`
*   Subinterval partitions: partition the range into non-overlapping sub-intervals by defining a sequence of equal distance break points, via `seq()`
*   Classification: classify each of the timestamps according to the sub-intervals, left closed and right open, via `cut()`
*   Frequencies: compute frequency of timestamps in each sub-interval via `table()`
*   Column binding: bind the sub-interval time and frequency columns via `cbind()`

Given that, `plot()` generates a simple line graph whose x-axis is the sub-interval time unit values (*i.e.* minutes or hours) and y-axis is the frequency of quotes which arrived in that sub-interval of time.

For those conducting high-frequency analysis, R packages suited for irregular-spaced methods include [zoo](http://cran.r-project.org/web/packages/zoo/index.html), [xts](http://cran.r-project.org/web/packages/xts/index.html), [its](http://cran.r-project.org/web/packages/its/index.html), [tseries](http://cran.r-project.org/web/packages/tseries/index.html), and [fts](http://cran.r-project.org/web/packages/fts/index.html).