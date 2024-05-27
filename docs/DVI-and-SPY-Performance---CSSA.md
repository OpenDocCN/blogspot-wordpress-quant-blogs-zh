<!--yml

category: 未分类

date: 2024-05-12 18:20:31

-->

# DVI 和 SPY 性能 | CSSA

> 来源：[`cssanalytics.wordpress.com/2010/07/29/dvi-and-spy-performance/#0001-01-01`](https://cssanalytics.wordpress.com/2010/07/29/dvi-and-spy-performance/#0001-01-01)

Michael 在 MarketSci 上对 DVI 进行了一些统计审查：[`marketsci.wordpress.com/2010/07/29/exploring-the-dvi-indicator-extreme-readings/`](http://marketsci.wordpress.com/2010/07/29/exploring-the-dvi-indicator-extreme-readings/) 。 MarketSci 所涵盖的测试仅适用于 1970 年以来的长期。 Michael 在展示 DVI 的整体工作方式上做得非常出色。 为了提供一些额外信息，DVI 在确定超买（> .5）或超卖（< .5）读数时考虑了两个因素：1）中间区间内收益的幅度和 2）中间区间内上涨日和下跌日的比例。一些平滑处理是有意进行的，以使指标成为“价值轴”，而不是像常规动量震荡器（RSI2、DV2、随机指标等）那样的峰值/谷值指标。 这在 MarketSci 最近的文章中的分析中有所体现。 平滑的 DVI 需要较长时间从超买转变为超卖，反之亦然。 这使其成为类似金叉的移动平均策略的极好补充。 下面是在中位数 .5 水平上多头/空头 DVI 的回测。 我们使用即将推出的工具 DVixl 生成了回测。 DVixl 是一个基于 Excel 的平台，非常实用且易于使用。 很快将提供详细信息。 请注意，DVI 在过去几个月中绝对压制了标准普尔 500 指数。

![](https://cssanalytics.files.wordpress.com/2010/07/dvi1.png)
