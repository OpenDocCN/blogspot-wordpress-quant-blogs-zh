<!--yml
category: 未分类
date: 2024-05-12 19:04:49
-->

# Quantitative Trading: Selecting tradeable pairs: which measure to use?

> 来源：[http://epchan.blogspot.com/2009/12/selecting-tradeable-pairs-which-measure.html#0001-01-01](http://epchan.blogspot.com/2009/12/selecting-tradeable-pairs-which-measure.html#0001-01-01)

***A guest blog by [Paul Farrington](http://www.paulfarrington.com/research/Selecting%20tradeable%20pairs.htm)***

One of the most important factors in statistical arbitrage pairs trading is the selection of the paired instruments.  We can use basic heuristics to guide us, such as grouping stocks by industry in the anticipation that stocks with similar fundamental characteristics will share factor risk and tend to exhibit co-movement.  But this still leaves us with potentially thousands of combinations.  There are some statistical techniques we can use to quantify the tradeability of a pair: one approach is to calculate the correlation coefficient of each pair's return series. Another is to consider cointegration measures on the ratio of the prices, to see if it remains stationary over time.

In this article I briefly summarise the alternative approaches and apply them to a universe of stock pairs in the oil and gas industry.  To measure how effective each measure is in real world trading, I back test the pairs using a simple means reversion system, then regress the generated win rate against the statistical results.  Some basic insights emerge as to the effectiveness of correlation and cointegration as tools for selecting candidate pairs.

Please visit http://www.paulfarrington.com/research/Selecting%20tradeable%20pairs.htm for details of my methodology and results.