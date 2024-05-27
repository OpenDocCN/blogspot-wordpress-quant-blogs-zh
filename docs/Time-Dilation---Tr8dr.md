<!--yml

类别：未分类

日期：2024-05-18 15:35:51

-->

# 时间膨胀 | Tr8dr

> 来源：[`tr8dr.wordpress.com/2009/12/18/time-dialation/#0001-01-01`](https://tr8dr.wordpress.com/2009/12/18/time-dialation/#0001-01-01)

2009 年 12 月 18 日 · 20:56

许多衡量标准在恒方差的波动率环境下效果最佳。这不是一个大的秘密。大多数回归因子，其中最简单的是永远受欢迎的移动平均线，在异方差序列的背景下尤其有偏见。

将异方差序列标准化为方差接近常数的最佳方法是注意以下几点。如果我们假设我们的过程大致是一个带有正态分布创新（或替代地，Hurst 常数接近 1/2）的 SDE，我们知道：

![](https://tr8dr.wordpress.com/wp-content/uploads/2009/12/picture-14.png)

作为一个粗略的衡量，我们可以通过按方差比例缩放我们的时间轴来去除大部分波动的波动。我使用基于持续时间的局部波动率衡量指标，带平滑或对于日数据，基于 EWMA 的评估：

![](https://tr8dr.wordpress.com/wp-content/uploads/2009/12/picture-23.png)

然后我们可以改变测度：

图片 3：![](https://tr8dr.wordpress.com/wp-content/uploads/2009/12/picture-33.png)

其中ψ(t)是一个平滑/缩放函数。此类缩放的一个例子（上窗格中的红色曲线表示与基线相比的缩放程度）：

![](https://tr8dr.wordpress.com/wp-content/uploads/2009/12/picture-62.png)
