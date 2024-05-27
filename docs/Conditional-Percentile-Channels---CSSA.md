<!--yml

category: 未分类

date: 2024-05-12 17:48:09

-->

# 条件百分位通道 | CSSA

> 来源：[`cssanalytics.wordpress.com/2015/02/20/conditional-percentile-channels/#0001-01-01`](https://cssanalytics.wordpress.com/2015/02/20/conditional-percentile-channels/#0001-01-01)

Ilya Kipnis 在 Quantstrat [最近发布了一些 R 代码](https://quantstrattrader.wordpress.com/2015/02/17/an-attempt-at-replicating-david-varadis-percentile-channels-strategy/)，试图复制永远受欢迎的[百分位通道战略](https://cssanalytics.wordpress.com/2015/02/08/a-simple-tactical-asset-allocation-portfolio-with-percentile-channels-for-dummies/ "一个“简单”的战术资产配置组合与百分位通道（适用于白痴）")。结果类似，但不完全一致，这可能与 Ilya 在评论中指出的百分位函数有关。无论哪种情况，总体精神保持不变，鼓励读者查看他对该策略的分析。

在量化金融中，有“[条件风险价值](http://www.investopedia.com/terms/c/conditional_value_at_risk.asp)”（CVaR）的概念，这是风险管理中经常使用的计算。其基本思想是你试图捕捉分布尾部的预期情况。与风险价值相比，CVaR 更全面，因为它不只看一个值。同样，百分位通道与风险价值在这个上下文中相似，以及传统的唐奇安通道，后者只关注一个参考价格。也许一个逻辑上的改进是，像 CVaR 一样使用某个百分位阈值以上的价格的平均值。这更像是计算价格的**预期**上限或下限。此外，为了考虑到最近的数据比较老的数据更重要的事实，我们可以相应地对这些价格进行加权。理论上，最重要的价格在极端处，也应该被相应地加权。所以条件百分位通道简单地是在百分位通道上增加了这两个思想。下面是如何计算的：

![条件百分位通道](https://cssanalytics.files.wordpress.com/2015/02/conditional-percentile-channels.png)

基本上，你选择一个阈值，比如`.75`和`.25`，然后根据时间位置（就像加权移动平均）和距离最大或最小值加权超过这些阈值的价格。这样，你就可以更准确地获得支撑和阻力的预期上限或下限（至少在理论上是这样）。我知道我会后悔的，但是在最近几篇文章中使用了相同的策略，即“百分位通道战略”，我替换成了条件百分位通道，使用的阈值仍然是`.75`和`.25`。其他参数都相同。下面是它的样子：

![条件百分位策略](https://cssanalytics.files.wordpress.com/2015/02/conditional-percentile-strategy.png)

看起来在收益和风险调整后的收益方面略有改善。总的来说，我更喜欢这个概念，因为它比唐奇安通道或百分位通道更多地概括了关于支撑/阻力的信息。它也是对移动平均线的一个很好的补充，后者捕捉了中心趋势，而不是价格在极端情况下的波动。所以你看，这又是对使用通道的另一种变化。
