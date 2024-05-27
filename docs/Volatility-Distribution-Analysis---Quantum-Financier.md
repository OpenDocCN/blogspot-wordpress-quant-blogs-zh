<!--yml

类别：未分类

日期：2024-05-18 14:04:34

-->

# 波动性分布分析 - Quantum Financier

> 来源：[`quantumfinancier.wordpress.com/2010/08/11/volatility-distribution-analysis/#0001-01-01`](https://quantumfinancier.wordpress.com/2010/08/11/volatility-distribution-analysis/#0001-01-01)

自从 Quantum Financier 博客最后一次有所动静已经很久了，但今天我回来了（虽然还没有回到家，但无论如何已经回到了博客圈！）。 今天的帖子将着眼于波动性的分布以及波动性的波动，试图探讨哪一个更稳定。 这里的结果暗示着与 CSS 最近的帖子 [Random Regime Musing](http://cssanalytics.wordpress.com/2010/08/04/random-regime-musings/) 相关；如果你还没有阅读过，我建议你去看看。

在帖子中，David 得出了以下结论：*“通过使用前向[波动性]估计，我们可以更快地对波动性的变化做出反应，以及它们将如何影响我们的均值回归策略”*。然后一个新的非常有趣的博客极客，[The Quanting Dutchman](http://quantingdutchman.wordpress.com/) 评论说波动性的波动通常更可预测。 这段对话引起了我的兴趣，我想我会把这个想法付诸实践。 以下统计数据是对不同样本大小的波动性和波动性的波动的比较，并在 500 个条的时间范围内进行了视觉比较。

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/08/volatility-analysis.png)

波动性

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/08/volatility-analysis-vol.png)

波动性的波动

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/08/volatility-analysis-volofvol.png)

数字似乎证实了理论，波动性的波动的分布似乎比普通波动的分布更稳定。 从这里，人们可以想知道是否增加的可预测性能够转化为改进的制度识别。 这个想法很吸引人，将在未来的帖子中讨论，我们还将探讨如何具体地使用这些信息并将其纳入交易策略。 你可能会发现我保持了我的分析非常肤浅。 请放心，这个主题将在接下来的一周内再次出现在博客上，我想深入探讨这一现象；更多信息将在之后呈现...

QF
