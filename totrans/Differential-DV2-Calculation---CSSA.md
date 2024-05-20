<!--yml
category: 未分类
date: 2024-05-12 18:53:11
-->

# Differential DV2 Calculation | CSSA

> 来源：[https://cssanalytics.wordpress.com/2009/07/29/differential-dv2-calculation/#0001-01-01](https://cssanalytics.wordpress.com/2009/07/29/differential-dv2-calculation/#0001-01-01)

**DV2 differential calculation:**

C, L, H= (close, low, high)
P= the percentrank function in excel default lookback of 250 days
Avg=the average
T=today (at the end of the day)
Y=yesterday

DV2 (not the unbounded version)=

***P(average(C/(H+L) for T,  C/(H+L) for Y))***

calculate this for ETF A and ETF B

the differential (D) is:

***D= P(DV2 for ETF A – DV2 for ETF B)***

if P is below .5 then Long ETF A, Short ETF B and vice versa. My advice is to wait for bigger discrepancies–ie .3/.7 for long/short