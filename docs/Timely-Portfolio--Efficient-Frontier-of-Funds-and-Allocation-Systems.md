<!--yml

分类：未分类

date: 2024-05-18 15:07:28

-->

# 及时投资组合：基金与分配系统的有效前沿

> 来源：[`timelyportfolio.blogspot.com/2012/04/efficient-frontier-of-funds-and.html#0001-01-01`](http://timelyportfolio.blogspot.com/2012/04/efficient-frontier-of-funds-and.html#0001-01-01)

我在[买入持有与战术系统的有效前沿](http://timelyportfolio.blogspot.com/2011/10/efficient-frontier-of-buy-hold-and.html)进行了一个基础实验，在那里我确定了标普 500 的有效前沿，其自身通过[Mebane Faber](http://www.mebanefaber.com/)的 10 个月移动平均战术分配进行了转换。

结果很有趣，但我没有进一步追求。现在，受到[系统投资者](http://systematicinvestor.wordpress.com/)的一些启发和工具，我想扩展这篇文章。这次我们将使用标普 500(VFINX)和美国债券市场(VBMFX)组合，同时使用由战术方法确定的投资组合（移动平均、RSI 和欧米伽）以及通过相同的战术方法转换的基金。我还是会像往常一样警告你们，这不是建议，而且几乎可以肯定会有大的损失。另外，我想指出，我已经用尽一切可能的方式检查了 10 个月移动平均值（甚至在 Excel 中手动检查），自 1990 年以来，它在 VFINX 上表现出色。在 1990 年之前，结果很好，但远不如 1990 年以后惊人。如果我有误，请告诉我。

[R 代码来自 GIST：](https://gist.github.com/2416288)
