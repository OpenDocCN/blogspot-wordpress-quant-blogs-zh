<!--yml
category: 未分类
date: 2024-05-12 18:48:58
-->

# Calculation: DV Super Smoothed Double Stochastic Oscillator | CSSA

> 来源：[https://cssanalytics.wordpress.com/2009/09/11/calculation-dv-super-smoothed-double-stochastic-oscillator/#0001-01-01](https://cssanalytics.wordpress.com/2009/09/11/calculation-dv-super-smoothed-double-stochastic-oscillator/#0001-01-01)

Hi all,  Corey Rittenhouse of Catallactic Analysis has been kind enough to test out some strategy variations on the DV Stochastic using the S&P500.  The combo strategy is very interesting. I forwarded him an example spreadsheet for the exact calculation of the indicator to post on his site. [http://www.catallacticanalysis.com/strategytests/differentstrategyvariationsDVSSDStochastic.php](http://www.catallacticanalysis.com/strategytests/differentstrategyvariationsDVSSDStochastic.php)

To calculate the double stochastic oscillator take the following steps:

1) take the stochastic of the last 10 days including high, low, and close data calculated as (today’s close- min(last 10 days HLC))/(max(last 10 days HLC)-min(last 10 days HLC))

2) take the stochastic of the number calculated in step 1, in this case (stochastic-min(stochastic last 10 days))/(max(stochastic last 10 days)-min(stochastic last 10 days))

3) take the 3 period (day) average of this result for the first smoothing

4) take .85 x the first smoothed value + .15 x the previous day’s smoothed value for to get the final result

The resulting stochastic is smooth and very responsive to the cycles that occur in the S&P500\. Good luck!