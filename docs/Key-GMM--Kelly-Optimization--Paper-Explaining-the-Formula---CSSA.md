<!--yml

category: 未分类

date: 2024-05-12 18:17:59

-->

# Key GMM (Kelly Optimization) Paper Explaining the Formula | CSSA

> 来源：[`cssanalytics.wordpress.com/2010/09/21/key-gmm-kelly-optimization-paper-explaining-the-formula/#0001-01-01`](https://cssanalytics.wordpress.com/2010/09/21/key-gmm-kelly-optimization-paper-explaining-the-formula/#0001-01-01)

在最初应用于体育博彩（离散投注）的凯利准则和基于连续时间的 Ed Thorp 的金融市场凯利准则之间存在一些混淆。金融凯利应用是从后者派生出来的，以解释市场上存在的未定义的收益或损失。应用于投资组合优化的金融凯利应用方法与传统的均值-方差优化方法有一些相似之处，即使用协方差矩阵来考虑资产之间的关系差异。然而，凯利方法旨在最大化复利回报，而经典优化则最大化算术夏普比率。基于几次询问，我决定提供链接超越原始 Thorp 论文：[`www.bjmath.com/bjmath/thorp/paper.htm`](http://www.bjmath.com/bjmath/thorp/paper.htm) Javier Estrada 撰写了一篇关于我称之为“GMM”或几何平均最大化的凯利优化关键论文。这篇论文可以在这里找到：[`www.fma.org/NY/Papers/Estrada-GMM.pdf`](http://www.fma.org/NY/Papers/Estrada-GMM.pdf) 。总之，数学并不特别难，但也不是像编程技术指标那样，需要使用协方差矩阵。这仅适用于技术和量化熟练的人，但可以使用统计软件如“R”（我们使用的就是 R）或 MATLAB 更容易地复制。

尽管如此，我们用于情感传播的方法基于特定应用是创新且独特的。聪明的人当然可以很大程度上复制所做的工作。关于创建跨市场组合的文章旨在展示经典投资组合理论如何帮助适应性信号聚合过程。这种方法不是线性的，它有助于解释回归经常未能明确通过最小二乘法解释的信号之间的关系。因此，输出更优，并为更复杂的使用提供了一个灵活的框架。
