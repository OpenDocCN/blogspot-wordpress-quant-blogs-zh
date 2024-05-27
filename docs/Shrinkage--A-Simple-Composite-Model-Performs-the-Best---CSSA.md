<!--yml

分类：未分类

日期：2024-05-12 17:56:39

-->

# 收缩：最简单的综合模型表现最佳 | CSSA

> 来源：[`cssanalytics.wordpress.com/2013/10/31/shrinkage-a-simple-composite-model-performs-the-best/#0001-01-01`](https://cssanalytics.wordpress.com/2013/10/31/shrinkage-a-simple-composite-model-performs-the-best/#0001-01-01)

![收缩](https://cssanalytics.files.wordpress.com/2013/10/shrinkage.png)

在过去的两篇文章中，我们讨论了使用[自适应收缩](https://cssanalytics.wordpress.com/2013/10/24/adaptive-shrinkage/ "自适应收缩")方法，同时也介绍了[平均相关收缩模型](https://cssanalytics.wordpress.com/2013/10/27/average-correlation-shrinkage-acs/ "平均相关收缩（ACS）")。真正的问题在于；在各种不同的模型中，哪种收缩方法效果最好？在从股票到资产类别甚至期货的多宇宙回测中，Systematic Investor 的 Michael Kapler 计算了每个收缩模型基于以下标准的综合得分：投资组合换手率、夏普比率、波动性和分散化，使用[综合分散化指标](https://cssanalytics.wordpress.com/2012/09/21/minimum-correlation-algorithm-paper-release/ "最小相关算法论文发布")（CDI）。更低的换手率是可取的，夏普比率显然越高越好，波动性越低越好，促进分散化越高越好。回测和代码可以在[这里](http://www.systematicportfolio.com/adaptive-shrinkage)找到。

考虑的模型如下：

![模型](https://cssanalytics.files.wordpress.com/2013/10/models.png)

表现最佳的收缩模型几乎任何有最基本 Excel 技能的人都可以实施：它就是样本相关矩阵、锚定相关矩阵（所有历史数据）和[平均相关收缩](https://cssanalytics.wordpress.com/2013/10/27/average-correlation-shrinkage-acs/ "平均相关收缩（ACS）")模型的简单平均值。这产生了对于资金管理者来说最理想特性的最佳组合。逻辑很简单：锚定相关矩阵提供了资产间关系的长时记忆，样本提供了短期/当前记忆，而平均相关收缩假设资产对其所有其他资产的平均相关性提供比样本更稳定的短期/当前估计。这是一个简单的实施例如何优于复杂的方法，只要概念是正确的。一般来说，只要可能，这是我偏好的方法，因为它在实际生活中更容易实施，更容易调试，更容易理解和解释。排名中的另一个有趣结果是，收缩模型的集成方法表现更好。这同样更有意义。适应性收缩模型（最佳夏普比率）相比之下表现较差——尤其是当考虑换手率作为因素时。可能仅使用 252 天窗口，或仅将夏普比率作为目标标准都是次优的。读者被鼓励尝试其他方法。(*我们确实调查了一些显示出很大前景的方法*)

最后，重要的是要认识到，无论使用哪种方法，收缩（shrinkage）都不是万能的。结果确实会更好，但与仅使用样本相关性相比，并没有天壤之别。使用收缩法得到的协方差矩阵低方差估计在实践中所能达到的效果是有限度的。为了提高性能，需要更精确的相关性预测器。
