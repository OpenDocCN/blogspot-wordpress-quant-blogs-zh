<!--yml

分类：未分类

日期：2024-05-18 15:37:11

-->

# 波动率估计的冒险之旅 | Tr8dr

> 来源：[`tr8dr.wordpress.com/2009/11/24/misadventures-in-variance-estimation/#0001-01-01`](https://tr8dr.wordpress.com/2009/11/24/misadventures-in-variance-estimation/#0001-01-01)

我一直研究不同的波动率模型，包括日波动率和日内波动率。在这个过程中，研究了**GARCH**(1,1)对日波动率的影响，并开发了多种基于持续时间波动率（**DV**）的日内模型。

**日收益率**我早就得出结论，GARCH(1,1)通常适合日数据，但对日内数据表现糟糕。不幸的是，对于某些市场，GARCH 表现同样糟糕。

我查看了过去 10 年加拿大的 2Y CMT 收益率。在任何给定年份，收益率都有显著的峰值。例如，在 2003 年，在原始日收益率上，GARCH 表现不佳（平方收益率：黑色，sigma 平方：红色）：

![图片 3](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-38.png)

作为一个实验，我使用（非常）轻微平滑的价格作为 GARCH 测试的基础。平滑使价格函数及其一阶导数（收益率）连续。在相同数据集上，但几乎无平滑的 GARCH(1,1)校准，提供了更高的拟合度（25 倍）：

![图片 4](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-44.png)

当然，我们现在将 sigma² 投影到轻微平滑的价格序列上，而不是原始序列。注意，随着平滑允许更平滑的过渡，收益的幅度也减少了。

让我们看看原始价格序列上的一小部分收益率：

![图片 1](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-19.png)

从视觉上看，平方收益率中似乎有一个自回归成分，但涉及跳跃，随后是收益接近零的时期。随后的跳跃似乎遵循近似线性衰减的幅度。你会注意到最后一组似乎是一个糟糕的拟合，然而，有一组低跳跃，在强度空间考虑时，将具有更高的组合值（即，考虑一个小窗口内的累积收益率）。

这种**行为将把这建模为强度函数**（相当于持续时间）。

**日内平方收益率**

流动期和清淡期的自相关图都显示出在 10 秒以上有显著的自相关，这表明我们应该在某个层面上寻找具有长记忆的 AR 过程：

![图片 1](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-110.png)

![图片 2](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-211.png)

迄今为止最成功的模型是一种基于持续时间的 Hawkes 过程，这种过程具有“无限”的自回归特性，并伴随指数衰减。
