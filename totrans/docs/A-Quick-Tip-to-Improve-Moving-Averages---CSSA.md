<!--yml
category: 未分类
date: 2024-05-12 18:42:39
-->

# A Quick Tip to Improve Moving Averages | CSSA

> 来源：[https://cssanalytics.wordpress.com/2009/11/11/a-quick-tip-to-improve-moving-averages/#0001-01-01](https://cssanalytics.wordpress.com/2009/11/11/a-quick-tip-to-improve-moving-averages/#0001-01-01)

Note that the “C” in CSS does not stand for “Countertrend” and I have spent plenty of time the last 2 months working on trend indicators and refinements. The essence of my evolving adaptive markets philosophy is to be agnostic with respect to trend or countertrend. That said, I have produced very little  published work so far on the former. Expect a whole new class of indicators in the months to come. Here is a simple method i have found extremely useful in cleaning up moving averages:

1) Take all price moves that are in the 90th or 95th and 10th or 5th percentile out of the data used for calculating the moving average especially if they represented unusual gaps.

2) The more recently these “outliers” occur, the more you have to weight current data to speed the average up to account for omissions. Thus exponential weighting is preferable if a large portion of a recent move was eliminated.

The Result: better moving averages with less trades and less false signals!