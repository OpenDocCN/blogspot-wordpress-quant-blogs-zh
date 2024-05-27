<!--yml

category: 未分类

date: 2024-05-18 14:02:09

-->

# 新策略绩效总结 – 量子金融家

> 来源：[`quantumfinancier.wordpress.com/2010/09/24/new-strategy-performance-summary/#0001-01-01`](https://quantumfinancier.wordpress.com/2010/09/24/new-strategy-performance-summary/#0001-01-01)

上周我说过我将会改变我策略绩效总结的设计，以便在博客圈更好地进行比较，所以这是第一个例子，我加上了它。

这个策略也是为了显示，有时我们如此专注于美国证券市场，以至于我们错过了某些有吸引力的投资机会。实际上，我在这方面尤其有罪。我通常在我的研究中研究标普 500 及其期货。然而这一次，我转而研究加拿大政府债券的 ETF（雅虎股票代码：XGB.TO），它是在我的某节课上介绍给我的。我测试了一个简单的 DV2 策略，使用.5 的入场/出场，并双向交易了这个策略。以下是结果。

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/09/xgb-to-dv2-res-e1285370478552.png)

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/09/xgb-to-strat-monthret-e1285370490959.png)

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/09/xgb-to-strat-res1-e1285370398641.png)

对于这样一个简单的策略，其结果令人印象深刻，风险与回报的比例也非常好，我通常不会分享效果这么好的策略，但因为它很简单，我想为什么不呢。然而，要小心这个，交易成本肯定会影响性能。作为一个结束的想法，我鼓励你在正常不会寻找交易想法的地方寻找，因为你可能会对结果感到惊讶。

最后，在我讨论[新策略报告](https://quantumfinancier.wordpress.com/2010/09/10/improved-key-perfomance-statistics/)的帖子中，Freeman 留言并提出了一个有见地的观点：

*QF-对于 Sortino Ratio，为什么不将 MAR 设为所考虑期间基准的历史回报率呢？考虑到与任何策略相关的机会成本，将可接受回报率设定为 0 似乎不太现实。上述建议（尽管很简单）是考虑在策略执行时可能拥有的假设性替代方案之一。*

所以基本上，这是一个权衡问题，我们要么基于超额回报来计算 Sortino 比率，要么简单地取下游离回报率。两者都有优点，如果我们使用超额回报，我们会考虑交易策略的机会成本与持有基准指数的机会成本之间的比较。如果我们决定使用正常回报序列来计算比率，我们可以将其与目前计算的 Sharpe 比率（Rf = 0%）进行比较。我们基本上会得到一个只用下游离回报率计算的 Sharpe 比率（即没有对上行波动的惩罚）。另外，我也可以使用超额回报序列来计算这两个指标。我希望读者能就这个问题给我反馈，所以如果你能在评论部分告诉我你更喜欢哪种比率，以及你对新的绩效总结整体有何看法，这将有助于我为您做得更好！

量化金融（QF）
