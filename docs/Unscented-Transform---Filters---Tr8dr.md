-->yml

类别：未分类

日期：2024-05-18 15:29:50

-->

# 无迹变换与滤波器 | Tr8dr

> 来源：[`tr8dr.wordpress.com/2011/07/28/unscented-transform-filters/#0001-01-01`](https://tr8dr.wordpress.com/2011/07/28/unscented-transform-filters/#0001-01-01)

无迹变换（滤波器）是为估计隐藏状态系统的条件分布函数而开发的实用替代蒙特卡洛采样。我们希望确定给定观察值（Yt）的隐藏状态（Xt）：

![](https://tr8dr.wordpress.com/wp-content/uploads/2011/07/screen-shot-2011-07-27-at-7-01-57-pm.png)

确定此分布 p(Xt | Y1:t)的顺序 MC 方法如下：

![](https://tr8dr.wordpress.com/wp-content/uploads/2011/07/screen-shot-2011-07-28-at-9-43-31-am.png)

这对我们来说行之有效，因为我们知道观察值 y[1:t]，并且应该对给定 Y 的状态 X 的似然性有一个看法，通过函数 g(.)将 X 的样本投影到 Y 上。确定似然性和减少所需的粒子（样本）数量，以得到健壮的积分（如 SIR）有各种方法。

基本蒙特卡洛粒子采样算法如下：

1.  从 f(X[t-1] + 噪声)生成 N 个 X[t]的样本，通过该 f(.)函数从 X[t-1]变换到 X[t]

1.  确定“粒子”为 p(Yt | X'[t],i) / 归一化常数，其中 p(Yt|Xt)可以通过应用函数 g(x)并确定计算出的 Yt 给定 Xt 的似然性来确定。

1.  根据算法，可能会进行一些重采样和核加权选择。

1.  均值是 Xt’s 的概率加权平均值（如上积分所示）

我过去实现并使用过这些的许多变体。对于复杂分布（例如多模态分布），蒙特卡洛方法是不可避免的。话说回来，粒子滤波器的速度可能比卡尔曼滤波器家族慢几个数量级。

**无迹变换** 于是，无迹变换应运而生。与 SMC 方法类似，无迹变换通过采样来确定分布的均值和高阶矩：p(x[t] | y[1:t])。而不是生成大量随机样本，无迹方法是围绕当前均值取特定点的样本。

无迹方法还避免了系统函数的非线性的近似，而是寻求确定更简单的问题：近似分布。围绕均值确定 2^d + 1 个样本（或 sigma）点并通过非线性函数变换，以得到状态向量的分布视图。

![](https://tr8dr.wordpress.com/wp-content/uploads/2011/07/orthogonal-projections.png)

如 Julier 和 Uhlmann 1997 年的开创性论文所示：

![屏幕快照 2011-07-28 下午 2.06.56](https://tr8dr.wordpress.com/wp-content/uploads/2011/07/screen-shot-2011-07-28-at-2-06-56-pm.png)

围绕均值确定的 sigma 点（Si 及其相关的权重 Wi），通过非线性系统函数进行转换，使我们能够确定分布 p(μ, P)的矩，其中μ是均值，P 是协方差（更高阶的矩也可以计算）：

![屏幕快照 2011-07-28 下午 2.26.28](https://tr8dr.wordpress.com/wp-content/uploads/2011/07/screen-shot-2011-07-28-at-2-26-28-pm.png)

然后，问题变成了如何选择这些围绕均值 Xt 的 sigma 点 Si。我们知道我们想要选择 Si = Xt + Ei，其中每个向量 Ei 在给定维度上提供了适当的扩散，沿着分布的方向。如果这些点选择得当，将提供足够的信息来重构分布的矩。

在假设 Xt（预转换）是椭圆分布的情况下，结果表明协方差矩阵的奇异值分解的列向量指定与分布轴共线的向量。这些向量如下确定并缩放：

![屏幕快照 2011-07-28 下午 3.40.45](https://tr8dr.wordpress.com/wp-content/uploads/2011/07/screen-shot-2011-07-28-at-3-40-45-pm.png)

有关更多详细信息，请阅读以下[论文](http://www.google.com/url?sa=t&source=web&cd=1&sqi=2&ved=0CBUQFjAA&url=http%3A%2F%2Fciteseerx.ist.psu.edu%2Fviewdoc%2Fdownload%3Fdoi%3D10.1.1.46.8107%26rep%3Drep1%26type%3Dpdf&ei=Xq8xTo3UNcKcgQe6quH5DA&usg=AFQjCNHo8y-X15XiCLoWuN3dkgrxCE55Tg&sig2=IpOnVHReCpwtSWEEUmqI2g "一种一致性、去偏差的极坐标与笛卡尔坐标转换方法").

**为什么选择 UKF**？

典型的 EKF 实现使用在分布更新中对线性（有时是二次）近似的扩散。除非你的系统在 1 阶动力学方面表现良好，否则这可能会失败得非常壮观（或者只是表现出显著的误差）。UKF 方法也不需要计算雅可比或海森矩阵，对于某些问题这可能非常困难或不可能提供。

**下一步**我特别感兴趣的是带有平滑的前向-后向 UTF。我发现对先验（不仅仅是立即的 t-1）进行平滑可以提供更佳的当前和下一期的预报。接下来我将写更多有关这一点的内容。
