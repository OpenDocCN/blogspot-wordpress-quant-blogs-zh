<!--yml

分类：未分类

日期：2024-05-12 18:35:58

-->

# Trade With The Trend: Using AggM as a Filter for Short-term Mean Reversion Indicators | CSSA

> 来源：[`cssanalytics.wordpress.com/2010/02/17/trade-with-the-trend-using-aggm-as-a-filter-for-short-term-mean-reversion-indicators/#0001-01-01`](https://cssanalytics.wordpress.com/2010/02/17/trade-with-the-trend-using-aggm-as-a-filter-for-short-term-mean-reversion-indicators/#0001-01-01)

在这个例子中，我们只允许顺着由 AggM（DVAM）定义的趋势进行交易，AggM 是一种可在 [www.dvindicators.com](http://www.dvindicators.com) 获得的复合趋势/均值回归指标。当 AggM 升至 65 以上时触发多头交易，并在 AggM 收盘价低于 35 时结束。在这个时间段内，我们只从多头一侧交易 DVO，入场价低于 50，出场价高于 50。空头交易在 AggM 跌至 35 以下时开始，并在 AggM 收盘价高于 65 时结束。在这个时间段内，我们只从空头一侧交易 DVO，入场价高于 50，出场价低于 50。除去 1998 年，这种策略平均产生了强劲的回报和非常低的回撤。这种方法与其他指标（包括 RSI2）配合也很好。

![AggMSignal_DVO](https://cssanalytics.files.wordpress.com/2010/02/aggmsignal_dvo.png)
