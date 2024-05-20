<!--yml
category: 未分类
date: 2024-05-12 18:49:57
-->

# CVI+: An Introduction | CSSA

> 来源：[https://cssanalytics.wordpress.com/2009/09/02/cvi-an-introduction/#0001-01-01](https://cssanalytics.wordpress.com/2009/09/02/cvi-an-introduction/#0001-01-01)

The development of CVI+ was based on logic and observation. When I first started discretionary trading, I looked for breakouts from congestion ranges. I had a great deal of success with that strategy across a variety of instruments including stocks, commodities and currencies. I wasn’t looking at bases in the classical IBD sense, often i was simply looking at 2-3 week congestion periods regardless of where they occured within the 52-week range. I had no idea what backtests were at the time, and I simply traded this way because I read that a lot of traders had success doing it.

Fast-forward years later as a quant, and  system developer one of the most pressing problems of the day is to determine whether a given move will mean-revert or follow through. After developing the DV2 and other mean-reversion indicators, I wanted to figure out when they would be less likely to work. Even though I trade primarily using computers, and no longer look at charts, I noticed upon reviewing some losing trades that they occured under some of the same conditions under which I would have taken an opposite position as a discretionary trader. That is, in recent times I was often fading tight breakouts from congestion ranges. So I decided to create an indicator that captured such a setup.

Here are the two major concepts that I wanted to incorporate:

1) 10-day volatility including intraday ranges

2) some sort of breakout via the open vs yesterday’s close, the close today vs yesterday’s high or the close vs yesterday’s close

While the calculation is proprietary, as a guideline you would normalize the volatility from 0 to 1 and subtract that number from one and average it with a normalized measure of the breakout . The resulting indicator CVI+ranges from 0 to 1 with levels above .5 indicating expected trending behavior on the long side, and levels below .5 indicating expected mean-reverting behaviour. Testing this indicator across a variety of instruments including stocks, commodities, currencies and indices, shows that it is robust, and does in fact differentiate trending from countertrend behaviour. I will present some results shortly.