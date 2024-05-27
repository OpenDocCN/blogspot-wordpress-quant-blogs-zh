<!--yml

类别：未分类

日期：2024-05-18 15:58:58

-->

# VIX and More: New Feature #1: VIX Weekly Sentiment Indicator

> 来源：[`vixandmore.blogspot.com/2007/02/new-feature-1-vix-weekly-score.html#0001-01-01`](http://vixandmore.blogspot.com/2007/02/new-feature-1-vix-weekly-score.html#0001-01-01)

是时候开始在这个博客上添加一些常规特色内容了，当然，除了常规的粉彩 Excel 图表...

今天我引入了 VIX 周度情绪指标——或者如果你喜欢冗长的缩写，叫 VWSI。这个指标的目的是衡量 VIX 在未来几周的走势。实际上，这个指标已经证明是在 1-4 周预测 VIX 走势的一个有用工具。好坏与否，我不会拿出一堆统计数据来展示 VWSI 在各种回测期间的表现如何。相反，请考虑以下散点图，它显示了 2006 年各种 VWSI 得分两周的 ROI，这合理地代表了 VWSI 的预测能力：

![](http://i104.photobucket.com/albums/m163/bl82/WeeklyVIXScoreand2wkROI.gif)

影响 VWSI 得分最大的因素主要是各种振荡器计算。

[简单移动平均线](http://stockcharts.com/school/doku.php?id=chart_school:technical_indicators:moving_averages)

，

[商品通道指数](http://stockcharts.com/school/doku.php?id=chart_school:technical_indicators:commodity_channel_index_cci)

，

[Williams %R](http://stockcharts.com/school/doku.php?id=chart_school:technical_indicators:williams_r)

指标，以及其他指标。值得注意的是，周 VWSI 得分对上周的得分没有记忆。因此，尽管一个得分的价值可能在 1-4 周内有交易含义，但每个星期都会从零开始构建新的得分。因此，极端的 VWSI 得分很少持续超过一两周。

最后，下面的 VWSI 温度计应该相对容易理解，特别是如果你记住“看涨”和“看跌”的标签适用于 VIX，而不是更广泛的市场，后者通常与 VIX 呈负相关。2007 年 2 月 16 日结束的那周的读数为+1，这被认为是中立区域。上周的 VWSI 读数甚至是零。
