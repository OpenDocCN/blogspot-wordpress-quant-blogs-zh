<!--yml
category: 未分类
date: 2024-05-12 18:43:25
-->

# Introducing Composite Mean Reversion and Trend Following Measures: The Aggregate “M” Indicator | CSSA

> 来源：[https://cssanalytics.wordpress.com/2009/11/05/trend-or-mean-reversion-why-make-a-choice-the-simple-aggregate-m-indicator/#0001-01-01](https://cssanalytics.wordpress.com/2009/11/05/trend-or-mean-reversion-why-make-a-choice-the-simple-aggregate-m-indicator/#0001-01-01)

**Note:** *Apparently there were some questions about how to calculate Aggregate M, please email us at* [*dvindicators@gmail.com*](mailto:dvindicators@gmail.com) *to receive spreadsheet later this weekend. Note we use a cleaner version of data than Yahoo Finance adjusted for splits and dividends with verified closing prices. I have been made aware that the backtest results using Yahoo are different from ours (note we calculated the same values as our readers using Yahoo Finance), and that is because their data is not entirely accurate.*

The Aggregate M indicator is based on the concept that in the long term the market trends, while in the short-term the market is  noisy, and has a tendency to mean-revert. Why not combine the two concepts to keep life simple?  The Aggregate M  is supposed to reflect an adjusted median that is filtered for short term noise. The median is a far more accurate measure of central tendency than a simple average especially with noisy data.  Taking a superior measure of trend and filtering out some of the noise by adjusting for short-term mean reversion creates an even better median. The Aggregate M is now both trend and mean-reversion rolled into one. In the example below the aggregate M is simply the average of 1) 252 day PERCENTRANK of High, Low and Close values and 2) 10 day (1-PERCENTRANK) of High, Low and Close values. This average is smoothed using a .6 weight on today and .4 weight on yesterday. Is this robust? The S&P500 results over the last 4000 bars speak for themselves–high accuracy, good gains per trade and a nice equity curve. In a separate multimarket test with 20 markets going back to 1984, the Aggregate M did 27% CAGR through 2009\. Is it the best method…….probably not—I certainly didn’t spend any time optimizing or digging as I came up with it just yesterday. Furthermore the structure can be substantially improved. But pretty damn good for two common sense parameters!

[![SPYAggM5050](img/c7a360d43977167f9b24788a258b89ef.png "SPYAggM5050")](https://cssanalytics.files.wordpress.com/2009/11/spyaggm5050.png)