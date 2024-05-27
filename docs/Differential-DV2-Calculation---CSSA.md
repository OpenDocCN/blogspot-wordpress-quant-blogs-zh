<!--yml

category: 未分类

date: 2024-05-12 18:53:11

-->

# 差分 DV2 计算 | CSSA

> 来源：[`cssanalytics.wordpress.com/2009/07/29/differential-dv2-calculation/#0001-01-01`](https://cssanalytics.wordpress.com/2009/07/29/differential-dv2-calculation/#0001-01-01)

**DV2 微分计算:**

C, L, H=（收盘价，最低价，最高价）

P= Excel 中百分位函数的默认回顾期为 250 天

Avg=平均值

T=今天（在当天结束时）

Y=昨天

DV2（非无界版本）=

***P(average(C/(H+L) for T,  C/(H+L) for Y))***

对 ETF A 和 ETF B 计算这个

差分（D）如下:

***D= P(ETF A 的 DV2 - ETF B 的 DV2)***

如果 P 低于 .5，则做多 ETF A，做空 ETF B，反之亦然。我的建议是等待更大的差异-即长/短为 .3/.7
