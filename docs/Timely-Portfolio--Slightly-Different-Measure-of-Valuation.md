<!--yml

分类：未分类

日期：2024-05-18 15:01:48

-->

# 及时投资组合：估值的不同衡量方法

> 来源：[`timelyportfolio.blogspot.com/2013/01/slightly-different-measure-of-valuation.html#0001-01-01`](http://timelyportfolio.blogspot.com/2013/01/slightly-different-measure-of-valuation.html#0001-01-01)

我对那些陈词滥调的标准估值措施感到厌倦，有时我会尝试思考其他方法。其中一个想法是分析[肯·法希恩的市场（ME）到账面（BE）的百分位数断点](http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/Data_Library/det_me_breakpoints.html)。我们可以看到，根据年份，股票被认为相对于整个市场来说是如何便宜的。随着这些断点的提高，市场愿意支付更高的价格。反之，随着这些断点的降低，股票的价格也会降低，或者可以被认为是更便宜的。由于有 20 个第五百分位数，因此水平图可以为我们提供这个估值措施的总体良好视角。

以下是自 1926 年以来各个第五百分位数绝对 ME/BE 估值的水平图。

为了更具有代表性，让我们绘制一个 ME-BE / 历史平均值 - 1 的水平图。

为了再看一个非水平图，我们可以使用 xyplot。

从理论上讲，我认为这可能提供另一种衡量股票便宜程度的方法，但当然，还需要做大量研究。

[R 代码来自 Gist：](https://gist.github.com/4550147)
