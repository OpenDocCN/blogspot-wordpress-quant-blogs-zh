<!--yml
category: 未分类
date: 2024-05-12 18:42:28
-->

# Reader Suggestion For “A Quick Tip on Moving Averages” | CSSA

> 来源：[https://cssanalytics.wordpress.com/2009/11/12/reader-suggestion-for-a-quick-tip-on-moving-averages/#0001-01-01](https://cssanalytics.wordpress.com/2009/11/12/reader-suggestion-for-a-quick-tip-on-moving-averages/#0001-01-01)

Hi, one of our quant-oriented readers whose nickname is coincidentally “Quant” made a great suggestion regarding my suggested refinement. Quant says that instead of eliminating outlier values (above the 95th and below the 5th percentile by range) I should at least account for them by giving them a maximum or minimum value.  The distortion created by eliminating them entirely would have less effect with a long moving average and a stock index, but with individual stocks and shorter moving averages this poses a problem. Along this line, I propose giving outlier values a maximum value that corresponds to the 80th percentile, and a minimum value that corresponds to the 20th percentile. In the future I will also discuss the importance of making these adjustments for more recent data vs past data.