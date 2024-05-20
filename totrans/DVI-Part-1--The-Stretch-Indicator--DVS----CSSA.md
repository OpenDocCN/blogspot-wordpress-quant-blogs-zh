<!--yml
category: 未分类
date: 2024-05-12 18:52:37
-->

# DVI Part 1: The Stretch Indicator (DVS) | CSSA

> 来源：[https://cssanalytics.wordpress.com/2009/07/31/dvi-part-1-the-stretch-indicator-dvs/#0001-01-01](https://cssanalytics.wordpress.com/2009/07/31/dvi-part-1-the-stretch-indicator-dvs/#0001-01-01)

The DVI is an intermediate oscillator which is a subset of the DVIO (like DVO, it is a flexible and adaptive indicator). There are several complementary components to the DVI, that aid in identifying intermediate overbought and oversold opportunities. Keep in mind that intermediate or long term oscillators have a hard time differentiating between long-term trends and true exhaustion points. As a consquence research shows that several factors seem to be present at exhaustion points (see the preview for the DVI), and stretch is one them.

The stretch indicator- DVS is valuable even on its own, and is essentially an oscillator that represents the number of days that the stock or ETF is stretched (not consecutively). Like the DVO, the DVS indicator is scaled using the PERCENTRANK function with a default lookback of 1-year. The equation is as follows:

If today was an up day, than +1, if it was a down day than -1\. This is the DS or daily score.

DVS= P(.5*sum(DS for the last 20 days)today+.5*sum(DS for the last 20 days)yesterday)

where P=percentrank with a lookback of 252 days or 1-year.

Surprisingly, this simple indicator does very well even using above below the mean (50th percentile). The suggested overbought/oversold bands would occur at 80 and 20.

I will post more detailed results when i can figure out how to embed excel tables (read:technophobia). But here are some interesting data points:

From 1995 to present:

***Buying the SPY after a down day:***

55% positive days .07% next day return

***Buying the SPY after a down day when the DVS is less than 50:***

57% positive returns .14% next day return

***Buying the SPY after a down day when the DVS is less than 20:***

59% positive returns .24% next day return

***Buying the SPY after a down day and the DVS is above 50:***

50% positive returns, -.02% next day return

***Buying the SPY after a down day and the DVS is above 80:***

48% positive days -.02% next day return

Results are even better when you use the DV2 instead of up/down days. As you can see the DVS is a consistent moderator of short-term returns, and if it is not aligned in the same direction (ie buying after down days when the market is overbought) it can subsume the shorter term mean reversion signal performance. In a future post we will look at how the DVS affects short signals, and also how it performs with in conjunction with the DV2.