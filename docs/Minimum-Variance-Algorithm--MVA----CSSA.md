<!--yml

分类：未分类

日期：2024-05-12 18:00:49

-->

# 最小方差算法（MVA）| CSSA

> 来源：[`cssanalytics.wordpress.com/2013/04/01/minimum-variance-algorithm-mva/#0001-01-01`](https://cssanalytics.wordpress.com/2013/04/01/minimum-variance-algorithm-mva/#0001-01-01)

经常有读者询问关于近似最小方差投资组合的方法。在实际操作中，只有长短投资组合的最低方差组合可以 closed form 计算，而长仓投资组合需要使用二次优化器来求解。长仓最小方差的源代码和示例可以在[Systematic Investor](http://systematicinvestor.wordpress.com/)找到——一个非常好的博客，还有一个包含许多标准优化方法的工具包。Systematic Investor 背后的男人 Michael Kapler（迈克尔·卡普勒）和我写了一篇关于寻找最小相关性的算法，称为[最小相关性算法](https://cssanalytics.wordpress.com/2012/09/21/minimum-correlation-algorithm-paper-release/ "最小相关性算法发布")（MCA），旨在近似[最大分散化投资组合](http://www.iijournals.com/doi/abs/10.3905/jpm.2008.35.1.40)。该算法与传统优化的主要优点是：1)计算速度快，计算简单 2)对估计误差的鲁棒性更强 3)风险分散更优。在各种宇宙的测试结果也显示，MCA 在风险调整回报方面优于其最大分散化对应物。最小方差算法（MVA）是 MCA 的近亲，并具有与传统最小方差优化相同的优点。在测试中，MVA 在大多数宇宙中显示了优于 MCA 的风险调整回报。尽管我尚未进行与传统最小方差相比的测试，但初步结果非常有竞争力。考虑到 MVA 非常简单易算，这令人鼓舞。本周稍后，我将介绍逻辑，并发布一个包含一些测试结果的电子表格。
