<!--yml

分类：未分类

日期：2024-05-12 18:32:39

-->

# 市场内的市场 | CSSA

> 来源：[`cssanalytics.wordpress.com/2010/04/05/markets-within-the-market/#0001-01-01`](https://cssanalytics.wordpress.com/2010/04/05/markets-within-the-market/#0001-01-01)

在上篇文章中，我试图强调市场和股票可以有自己的独特行为，而且使用不同的变量可以隔离它们。这样做可以带来广泛的机会：1) 找到最适合你交易风格的股票/市场 2) 通过控制这些效果实现更集中的分析 3) 允许我们创建内部宽度指标，这些指标更加准确。

在我们的研究中，一个突出的变量是股票或市场趋势的倾向。这个变量是 Livermore Active Issues Index 的核心组成部分，被称为“LTR”，代表 Livermore Trend Rank。请注意，这并不是一个基于相对强度的得分，而是一个较长时间内相对“趋势性”的历史测量值。然后我们将相对强度与 LTR 和成交量指标结合，创建最终的指数得分。虽然用于创建 LTR 的技术是专有的，但它并不涉及任何统计上复杂的内容。LTR 准确度高且非常稳健，并在 35 个不同的市场和所有主要股票指数的股票上证明了其有效性。**高 LTR 得分表明市场或股票预计将呈现趋势，而低 LTR 得分则表明市场或股票预计将回归平均值。** LTR 得分每月计算一次，不会频繁变动。这意味着行为不是暂时的波动效应，而是股票或市场趋势/回归平均值的中期或长期行为倾向。

下面我们展示了使用 LTR 因子将纳斯达克 100 指数的前 50%和后 50%分离的标准反转/反转日策略（下跌日做多，上涨日做空）的表现。[![LTRRank_Comp](https://cssanalytics.files.wordpress.com/2010/04/ltrrank_comp.png)](https://cssanalytics.files.wordpress.com/2010/04/ltrrank_comp.png)

正如您清楚地看到的，市场中有一半的股票倾向于趋势，而另一半则有强烈的倾向回归平均值。这对我们来说具有巨大的意义——尤其是考虑到指数本身 QQQQ 倾向于回归平均值。***这意味着我们可以更准确地预测 QQQQ 或 SPY 或其他 ETF/指数的方向，通过控制这个变量的效果。这也意味着你应该把不同的策略，如趋势或回归平均值策略，应用到指数的不同股票上，而不是试图创建一个通用的系统。***

![RFT_Top50LTR](https://cssanalytics.files.wordpress.com/2010/04/rft_top50ltr.png)

![](https://cssanalytics.files.wordpress.com/2010/04/rft_bottom50ltr.png)
