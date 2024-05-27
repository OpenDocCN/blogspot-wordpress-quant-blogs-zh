<!--yml

category: 未分类

date: 2024-05-12 18:08:24

-->

# 后续 FAQ：“无预测”算法和最小相关性算法 | CSSA

> 来源：[`cssanalytics.wordpress.com/2011/08/15/follow-up-faq-forecast-free-algorithms-and-minimum-correlation-algorithm/#0001-01-01`](https://cssanalytics.wordpress.com/2011/08/15/follow-up-faq-forecast-free-algorithms-and-minimum-correlation-algorithm/#0001-01-01)

针对上一篇文章[`cssanalytics.wordpress.com/2011/08/09/forecast-free-algorithms-a-new-benchmark-for-tactical-strategies/`](https://cssanalytics.wordpress.com/2011/08/09/forecast-free-algorithms-a-new-benchmark-for-tactical-strategies/)中的诸多评论和问题，我决定采用不太常见但更实用的方法，写一篇 FAQ 来回答这些问题，既是为那些友善地提出了理智贡献的人，也是为了新读者。请注意，有人提醒我说，同行博客作者 Quantivity 在相似的主题上写了一系列非常出色的文章：[`quantivity.wordpress.com/2011/04/10/portfolio-theory-is-dead-now-what/`](http://quantivity.wordpress.com/2011/04/10/portfolio-theory-is-dead-now-what/)

***什么是“无预测”算法？***

我应该澄清一下，因为这有点不准确。Strom Macro[`strommacro.wordpress.com/`](http://strommacro.wordpress.com/)在最近的一篇博客中对这个问题发表了一些评论。“无预测”在 CSS 中指的是一种不估计期望收益的方法。在投资组合算法的背景下，这意味着我们不关心关于资产类别（或股票）应该如何表现的相对或绝对结论。*这并不意味着我们不估计相关性和波动性——事实上，这些估计对算法至关重要*。实证误差表明，相关性和波动性的误差远低于收益输入的误差。这就是为什么金融工程师花了这么多时间在后者而不是前者上（工程师通常更感兴趣的是时间序列中最可预测的因素）。

2) ***算法是如何构建的？***

在这一点上，我应该提到我正在编写一份关于这个主题的白皮书（即将出版）。最小相关性组合（MCP）将是本文的主题，并且基准构建将详细阐述。它使用了更传统的优化/迭代方法，并加入了一些有趣的变化。相比之下，最小相关性算法（MCA）是一个算法——它是一个旨在更快更稳健的启发式/计算解决方案，但也是专有的。也就是说，MCP 的性能非常接近 MCA，并且两者都基于相同的概念。

3) ***算法对资产类别或市场的选择是否非常敏感？***

不是。这就是“无需预测”的方法的不同之处-市场选择和参数长度都表现出比经典的“GTAA”方法少得多的变化。这是因为：a）它们生成的投资组合更为分散，成分之间的相关性更小 b）波动率和相关性可以从几乎任何时间段很好地外推，而价格或收益或相对收益/排名的趋势在更长的间隔里表现最好。因此，虽然相对强度/动量和趋势跟随是稳健的方法，但我认为“无需预测”的算法更加稳健。

4) ***最小相关性算法是风险平价的一种变体吗？***

不是。风险平价方法假定组合风险的风险贡献是相等的，它是最小方差方法和等权方法的混合。最小相关性算法旨在优化风险贡献，以减少投资组合的风险，并且仅仅关注于多样化带来的风险降低。这是我在论文中更详细解释之前最好的说法。

感谢所有优秀的评论和反馈-很快我将发布一篇关于这个主题的论文。对于那些希望在完成后直接收到论文的人，我将在博客上发布一个邮箱地址，您可以在那里请求第一份复印件。
