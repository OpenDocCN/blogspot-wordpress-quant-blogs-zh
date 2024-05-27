<!--yml

类别：未分类

日期：2024-05-12 17:49:59

-->

# NLV2：捕捉第三导数|CSSA

> 来源：[`cssanalytics.wordpress.com/2014/12/09/nlv2-capturing-the-3rd-derivative/#0001-01-01`](https://cssanalytics.wordpress.com/2014/12/09/nlv2-capturing-the-3rd-derivative/#0001-01-01)

![3rd derivative](https://cssanalytics.files.wordpress.com/2014/12/3rd-derivative.png)

在[上一篇文章](https://cssanalytics.wordpress.com/2014/12/03/combining-acceleration-and-volatility-into-a-non-linear-filter-nlv/ "结合加速度和波动性的非线性滤波器（NLV）")中，我介绍了结合波动性和加速度的非线性滤波器概念。然而，这只是利用非线性滤波器概念的一种配置。使用传统的波动性计算会给每个数据点分配相等的权重，实际上有些数据点应该比其他数据点有更高的权重。为了捕捉不同的权重函数，可以使用多个指标在波动性计算中给数据点加权，使其更能响应市场数据的传入。使用[加速度](https://cssanalytics.wordpress.com/2014/12/01/volatility-of-acceleration-part-two/ "加速度的波动性（第二部分）")是一个有趣的想法，可以减少滞后并迅速捕捉波动性的变化。初步分析在这方面显示出一些希望。加速度是第二导数，所以一个有趣的问题是第三导数**-**或者加速度的速度是否可以产生更好的结果。我创建了一个新的框架来捕捉非线性加权，这个框架更容易理解且易于实施：

A) 计算 B 中每日对数回报的平方与其平均回报的滚动序列

B) 计算对数回报差值（加速度/误差）的滚动绝对序列

C) 计算 B 中对数回报差值（绝对加速度/误差）的滚动序列，这是第三导数或加速度的速度。

D) 将 A 中的每个日值乘以当天的 C 值除以过去 10 天 C 值之和**-**

F) 求 D 中值的和**-**这是 NLV2

以下是 NLV2 在标普 500（SPY）上的表现与其他先前介绍的方法相比：

![nlv3](https://cssanalytics.files.wordpress.com/2014/12/nlv3.png)

![nlv4](https://cssanalytics.files.wordpress.com/2014/12/nlv4.png)

这种方法的表现曲线与其它方法迥然不同，虽然近年来其相对表现并不出色，但在整个测试期间，它一直是表现最佳的方法。尽管其他人可能会忽视近期表现不佳的事物，但我的研究认为这是一个错误——许多系统和方法都会围绕某个长期平均值进行回归。由于这种方法比 NLV 的移动部件少，因此它本质上更具吸引力，或许更加耐用。不管怎样，展示这种方法的目的是为了提供一种看待数据的不同方式——显然，不同对数回报的导数携带不同的信息片段，将这些信息结合起来，形成一个校准的预测模型或非线性滤波器，可能会在标准波动率公式之外带来额外的价值。
