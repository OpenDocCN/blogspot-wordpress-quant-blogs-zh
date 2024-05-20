<!--yml
category: 未分类
date: 2024-05-12 18:41:39
-->

# A New Performance Statistic | CSSA

> 来源：[https://cssanalytics.wordpress.com/2009/11/20/a-new-performance-statistic/#0001-01-01](https://cssanalytics.wordpress.com/2009/11/20/a-new-performance-statistic/#0001-01-01)

This was originally inspired in a response to reader “SeekingBeta” who also had a very good idea for a performance metric. The following was take from the Community Forums on the DV Indicators website: [http://www.dvindicators.com/community/forum/?vasthtmlaction=viewtopic&t=8.0#postid-44](http://www.dvindicators.com/community/forum/?vasthtmlaction=viewtopic&t=8.0#postid-44)

Here is the original  post (from me with a couple edits): 

“hi , you just inspired me to create a new metric DVFE based on the fractal efficiency of the equity curve. perfect efficiency would imply that the curve had no wasted movement, and although short-term profit spikes would be somewhat penalized (nonetheless this is desirable as a profit spike is generally transient and the result of an extreme market regime)–typical upside movement would not be penalized. to calculate this metric one would have to use a continuous equity curve and a fixed bet methodology to avoid a lognormal curve that would distort results.An adjustment is also made for the number of trades which is useful to help avoid rewarding strategies with very few trades.

**DVFE:** CAGRx(absolute value of fractal efficiency)x(1-(1/(the square root of the #of trades))

where fractal efficiency (Kaufman’s fractal efficiency) is the net change in the equity curve divided by the sum of the absolute value of daily changes in the equity curve.”

This new performance statistic helps overcome many of the drawbacks of the DVR which can penalize upside volatility. Theoretically, the DVFE says that if something is going up 100% in a perfect straight line, that is more desirable than something that is going up 10% in a perfect straight line. This makes logical sense…..though I would always look at the DVR as well since upside volatility is a useful indicator of how much something could fall when a strategy or stock breaks down. There is little question that proportionately the stock that goes up 100% in a straight line will likely fall farther and faster than the stock that is going up 10% in a straight line.