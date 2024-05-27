<!--yml

类别：未分类

日期：2024-05-12 17:50:27

-->

# 将加速度和波动性结合为非线性滤波器（NLV）| CSSA

> 来源：[`cssanalytics.wordpress.com/2014/12/03/combining-acceleration-and-volatility-into-a-non-linear-filter-nlv/#0001-01-01`](https://cssanalytics.wordpress.com/2014/12/03/combining-acceleration-and-volatility-into-a-non-linear-filter-nlv/#0001-01-01)

![nonlinear](https://cssanalytics.files.wordpress.com/2014/12/nonlinear.png)

最近的两个[帖子](https://cssanalytics.wordpress.com/2014/11/28/a-new-better-measure-of-risk-and-uncertainty-the-volatility-of-acceleration/ "A New (Better?) Measure of Risk and Uncertainty: The Volatility of Acceleration")介绍了一种将加速度作为替代风险度量的新方法。初步结果和直觉都表明，它值得考虑作为可以用于预测风险的另一种信息。虽然我提出了加速度是否比波动性更好的指标的问题，**更有用的问题应该是我们是否可以将这两者结合起来，或许比单独使用其中任何一个更好**。传统波动性显然更广泛地被使用，并且对解决传统投资组合优化至关重要。因此，它是作为基线指标的一个合乎逻辑的选择。

线性滤波器（如移动平均线和回归）生成的输出是输入的线性函数。相比之下，非线性滤波器生成的输出与输入呈非线性关系。非线性滤波器的示例包括多项式回归，甚至是简单的中值。非线性滤波器的目标是创建一种更优越的权衡数据的方式，以生成更准确的输出。通过使用非线性滤波器，可以大大减少滞后并增加响应速度。由于波动性是高度可预测的，因此我们希望尽可能地减少滞后并增加响应速度，以生成更优秀的结果。

那么我们如何创建一个包含加速度的波动性指标呢？答案是我们需要动态地根据加速度的大小对每个数据点的偏差平方进行加权，其中更大的绝对加速度应该在每个数据点上产生指数级别的更高加权。以下是如何计算 10 天 NLV 的方法（不要惊慌，我将在下一篇帖子中发布一个电子表格）：

A) 计算每日对数收益的平方偏差的滚动系列减去它们的平均收益

B) 计算对数收益的第一差值的绝对值的滚动系列（加速度/误差）

C) 使用 B 获取当天的值，并将其除以一些可选的平均值，如 20 天，以获得加速度的相对值。

D) 将 C 提升至 3 次方或您选择的某个常数- 这是相对加速度常数的滚动系列

E) 按照最近 10 天 D 值之和除以当前日的 D 值来加权 A 的每日值-

F) 将 E 中的计算除以加权常数之和（D 值之和除以它们的和） - 这就是 NLV，类似于传统加权移动平均数的计算

接下来是关键一击 - 这里是与[上一篇文章](https://cssanalytics.wordpress.com/2014/12/01/volatility-of-acceleration-part-two/ "Volatility of Acceleration Part Two")中提出的不同备选措施相比的结果：

![nlv](https://cssanalytics.files.wordpress.com/2014/12/nlv.png)

![nlv2](https://cssanalytics.files.wordpress.com/2014/12/nlv2.png)

这个概念作为一个结合了加速度的波动性的混合度量显示出了潜力。一般的计算可以应用于许多不同的方式，但这种方法相当直观和通用。在下一篇文章中，我将展示如何使这个非线性滤波器对波动性的变化更加敏感。
