<!--yml

分类：未分类

日期：2024-05-12 20:34:09

-->

# Falkenblog: 低波动性战术重要吗？

> 来源：[`falkenblog.blogspot.com/2012/03/do-low-vol-tactics-matter.html#0001-01-01`](http://falkenblog.blogspot.com/2012/03/do-low-vol-tactics-matter.html#0001-01-01)

对于任何策略来说，一个重要的问题是战术的重要性有多大。也就是说，对于某些策略，战术并不重要，因为算法具有“平坦最大值”，其中许多参数产生的输出几乎与最优参数一样好。债务模型具有这种特性，因为少数输入在各种权重和转换下都能很好地生成最优指标。

关于低波动性投资，有多种投资方式。首先，你可以选择过去 N 天内波动性最低的股票，并构建一个投资组合。这就是

[SPLV](http://www.invescopowershares.com/products/overview.aspx?ticker=SPLV)

ETF 采取的方法。或者你可以选择贝塔值最低的股票。然后，还有因子方法，它对一组从股票横截面提取的潜在因子应用均值-方差优化。标准约束优化算法可以应用于这个问题。还有其他方法，比如

[LVOL](http://www.russelletfs.com/Products/LVOL_Index.aspx)

ETF 选择与低波动性投资组合代理紧密匹配的股票，但我发现这有点过于复杂。

无论如何，我选取了 1500 只非 ETF 美国股票，并使用截至 2011 年 2 月的日数据应用了贝塔值、波动性和因子方法，然后观察了接下来一年中这些投资组合的表现。每个投资组合大约包含 100 只股票，它们之间大约有 65 只股票重叠。相对于其来源的等权重基准，波动性降低了约 45%。相比之下，价值和成长策略的轨迹则大相径庭。这表明，如果你只是追求低波动性，特定的算法并不重要。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjO2UBBfgPgpx7EK2NpMr-8D1yMvG4pgKOcXk-d2Z29GBOLfkqKVI2qXMpB30vXQ1YE7xPDIGj3cX1o4tfWjFcZqymJhJrNpi59PWouXNyW9DEHSV8xyX7SUi7oM8g4vv_rnzWs3A/s1600/totret2.png)
