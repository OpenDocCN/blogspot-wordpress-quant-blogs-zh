<!--yml

类别：未分类

日期：2024-05-12 17:56:56

-->

# 平均相关收缩（ACS）| CSSA

> 来源：[`cssanalytics.wordpress.com/2013/10/27/average-correlation-shrinkage-acs/#0001-01-01`](https://cssanalytics.wordpress.com/2013/10/27/average-correlation-shrinkage-acs/#0001-01-01)

在上一篇关于[自适应收缩](https://cssanalytics.wordpress.com/2013/10/24/adaptive-shrinkage/ "自适应收缩")的文章中，介绍了平均相关收缩（ACS）模型，并将其与其他标准收缩模型进行了比较。可以在此处找到演示如何实施 ACS 的电子表格：[平均相关收缩](https://cssanalytics.files.wordpress.com/2013/10/average-correlation-shrinkage.xlsx)。这种方法旨在成为替代性收缩模型，可以混合使用或用于替代标准模型。最受欢迎的模型之一是“常相关模型”，它假设资产之间存在恒定的相关性。这个模型的优点是它是一个非常简单和结构良好的估计器。弱点是它过于死板，其性能取决于宇宙中相似相关与不相关资产的数量。平均相关收缩提出，资产的成对相关性的一个良好估计器是其与其他所有资产的成对相关性的平均值。对于任何一对资产，它们的新的成对相关性是它们分别与所有其他资产的平均相关性的平均值。这是直观的，并且平均值对错误不太敏感，而单个相关性估计值则更少受限制，因为它不假设所有相关性都相同。

下图描述了样本与平均相关矩阵之间的关系：

![平均相关收缩](https://cssanalytics.files.wordpress.com/2013/10/average-correlation-shrinkage.png)

由上图可见，平均相关矩阵倾向于降低高相关资产的相关性，并增加低相关资产的相关性。可以使用以下公式将平均相关矩阵与先前的样本相关矩阵以一定比例加权：

**调整后的相关矩阵**=w*（平均相关矩阵）+（1-w）*样本相关矩阵

通过使用这种收缩方法调整优化的相关性输入，得到的权重对低相关资产的倾向较小，而对高相关资产的倾向较大，这些资产更有可能被纳入最终投资组合。像所有收缩方法一样，这意味着某种妥协

下图描述了使用收缩因子![（w）](img/b26a9cd9652d6f591c6ea7df09c0d8cf.png)为 0.5 的最终调整后的相关矩阵：

![调整后的相关矩阵](https://cssanalytics.files.wordpress.com/2013/10/adjusted-correlation-matrix.png)
