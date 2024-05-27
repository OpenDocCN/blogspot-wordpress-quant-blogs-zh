<!--yml

类别：未分类

日期：2024-05-18 15:06:06

-->

# 及时投资组合：PIMCO 基金的美好相关性地图

> 来源：[`timelyportfolio.blogspot.com/2012/06/pretty-correlation-map-of-pimco-funds.html#0001-01-01`](http://timelyportfolio.blogspot.com/2012/06/pretty-correlation-map-of-pimco-funds.html#0001-01-01)

随着[PIMCO 拓展至固定收益之外](http://www.pimco.com/EN/Insights/Pages/Neel%20Kashkari%20Discusses%20PIMCO%20Equity%20Platform.aspx)，我认为研究 PIMCO 共同基金与标普 500 的相关性可能会有所帮助。不幸的是，由于基金数量庞大，我无法使用 PerformanceAnalytics 的图表。相关性。我认为我已经制作了一张 PIMCO 机构股票基金（成立时间在 5 年之前的）的美好相关性热力图。当然这排除了许多新的策略，但在代码中调整列表很容易。我添加了先锋标普 500 基金（VFINX）作为参考点。然后，我按照与 VFINX 的相关性对热力图进行了排序。

如预期的那样，基金分为两个相当不同的群体：那些（主要是固定收益）与标普 500 相关性为负/低，以及那些具有强烈正相关性的基金。

以下是带有树状图排序的标准热力图，虽然它有其用处，但看起来有点忙碌。

如果我们只关心与标普 500（VFINX）的相关性，那么这可能更有帮助。

（R 代码来自 GIST：[`gist.github.com/2931640`](https://gist.github.com/2931640)）
