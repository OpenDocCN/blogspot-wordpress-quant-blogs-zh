<!--yml

分类：未分类

日期：2024-05-18 04:46:28

-->

# 智能交易：使用 R 语言的时间序列日历热力图

> 来源：[`intelligenttradingtech.blogspot.com/2010/02/time-series-calendar-heat-maps-using-r.html#0001-01-01`](http://intelligenttradingtech.blogspot.com/2010/02/time-series-calendar-heat-maps-using-r.html#0001-01-01)

我偶然发现了一个有趣的博客，展示了

[在 R 中绘制时间序列日历热力图](http://blog.revolution-computing.com/2009/11/charting-time-series-as-calendar-heat-maps-in-r.html)

。它是基于 Humedica 的 CMO Paul Bleicher 创建的伟大算法。我让你链接到其他博客，以查看有关背景和原始源代码的更多详细信息。

我对代码进行了微小的修改，以允许%日变动，而不是价格值。

`stock.dailychangecalendarHeat(stock.data$Date[1:length(stock.data$Date)-1], stock.dailychange, varname="SPY daily % changes(CL-CL)")` ![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhTtPKOCD7b2lZnkon7RPPVS1TLP-8lbIb2DXj8ZXDuJRfmnTqY98T7rQDJE7ExnOCV7xN-VWbNTzSePGdnH4usVpSjJwFJLMzb0OOwMtZCTHhca-mA4FxlU6RT_LqK88W8NwLxaW5mKfc/s1600-h/spy_ex.jpg)

图 1. SPY 时间序列的日历热力图 2005-至今

有趣的是，你可以看到异常事件往往会**聚集**（异方差性），并且在接近平均分布时，变化较小的日子较多。利用聚集区域可能会帮助预警即将到来的灾难性市场状态（如 2008 年底所示），这与使用 VIX 作为代理指标相似。此外，从 10,000 英尺的高度俯瞰，可能会让你发现需要进一步评估的有序区域。
