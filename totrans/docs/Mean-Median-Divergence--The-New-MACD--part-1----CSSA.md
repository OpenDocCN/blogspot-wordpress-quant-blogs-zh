<!--yml
category: 未分类
date: 2024-05-12 18:51:41
-->

# Mean/Median Divergence– The New MACD?(part 1) | CSSA

> 来源：[https://cssanalytics.wordpress.com/2009/08/06/meanmedian-divergence-a-great-trend-indicator-part-1/#0001-01-01](https://cssanalytics.wordpress.com/2009/08/06/meanmedian-divergence-a-great-trend-indicator-part-1/#0001-01-01)

It has been well documented that short-term and intermediate-term moving average systems have lost their “zip” in recent years—partially this has to do with the increased tendency toward mean reversion, but i also believe that one of the reasons also has to do with  “trader effects.” (a term coined in “The Way of the Turtle”) Trader effects simply refers to the fact that too many traders using the same tool will tend to reduce the value of a given indicator. Worse still, the volatility of signals given by these indicators also increase. The same fate has happened to the classic MACD, an indicator designed by Gerald Appel. The actually idea was inherently sound– the concept of the MACD borrowed principles from engineering to detect acceleration. Over the years as people caught on, the advantage of early trend detection was watered down by trader effects.

Refinements can be made to basic indicators that can revive their profitability while keeping the underlying concept intact. Some of the best refinements are simple and take into account the inherent flaws in their component parts. One of the problems with moving averages for example has to do with outliers. Large values that occur at any point in the data series can distort the real trend. Assuming 10 students take a test with test scores as follows:

100, 91, 58, 44, 57, 51, 53, 59, 53, 55

The average is actually 62%, the problem is, 80% of the students were “below average.” The distortion is caused by the two high scores, while in actuality most students did poorly on the test.  The median in this case is 56%, and 50% of students were below this number. Ok so this is stats 101, but so what? The fact is, no standard indicators or tools that i know of take a look at the difference. Most indicators use averages, most portfolio managers and traders look at averages, and if you look at median values then you are standing apart from the crowd. This fact gives you an advantage: [http://traderfeed.blogspot.com/2009/08/trading-creatively-finding-new-niches.html](http://traderfeed.blogspot.com/2009/08/trading-creatively-finding-new-niches.html)

Using mean/median divergence is a valuable way to spot trends early on. While moving averages are falling, the median price may actually be rising–indicating that most prices recently have been moving up. The way i calculate mean/median divergence is as follows:

***median*** of the last “n” days***– average*** of the last “n” days = ***D***

I actually prefer to smooth ***D*** using a moving average between 2 to 5 days.  If ***D*** is above zero, this triggers a buy, if it is below zero that triggers a sell. Good results also come from buying when ***D*** is rising, or selling when it is falling. The astute trader will combine both and use different periods- one short, one long. Note that ***D*** also functions as an excellent early trend filter for pure trend systems using breakouts or moving averages. Of course, you would have to match a shorter-term trend system than the ***D*** to make it work.

To create a new MACD–we will call it the MMDI (Mean Median Divergence Indicator), you would simply substitute the median for the short-term moving average (12), and produce the calculation the exact same way using a 26-day SMA/EMA, and taking the 9-day SMA/EMA of the ***D (12-day median minus 26-day average).*** The new MACD using the median outperforms the old MACD, and using shorter time frames the new MACD is highly useful at detecting fast shifts in momentum. ***NOTE : THAT THE RESULTS ASSUME LONG WHEN  MACD>0, SHORT WHEN MACD<0***

| Annualized Return last 3000 bars |
|   | New  | Old |
|   | MMDI | MACD (sma) |
| Nasdaq | 9.4% | 2.4% |
| S&P500 | 7.5% | 1.0% |
| Russell | 12.9% | 7.6% |
| Barrick Gold | -21.4% | -25.7% |
| Exxon Mobil | -8.7% | -12.7% |

As we can see this is a consistent improvement over the old MACD. It appears that the simple change of using the median in the short-term average made a difference.  Different settings produce results in the same direction.  While im not a fan of standard indicators per se, my point is that some basic knowledge of statistics and some intuition can help produce superior results. The key is in the concepts, not in “magical settings.” It also helps to use different indicators than the competition. Ultimately, if too many traders use the same indicator, with the help of computers, they will quickly discover the best settings.