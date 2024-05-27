<!--yml

category: 未分类

日期：2024-05-12 17:50:46

-->

# 加速度波动 第二部分 | CSSA

> 来源：[`cssanalytics.wordpress.com/2014/12/01/volatility-of-acceleration-part-two/#0001-01-01`](https://cssanalytics.wordpress.com/2014/12/01/volatility-of-acceleration-part-two/#0001-01-01)

![acceleration 2](https://cssanalytics.files.wordpress.com/2014/12/acceleration-2.png)

在[上一篇文章](https://cssanalytics.wordpress.com/2014/11/28/a-new-better-measure-of-risk-and-uncertainty-the-volatility-of-acceleration/ "一种新（更好？）的风险和不确定性度量方法：加速度波动")中，我介绍了一种基于每日收益加速度来计算风险或不确定性的不同方法。思考这个度量方式的另一种方式是它考虑了使用昨日收益预测今日收益的平均误差。利用误差创建更好的趋势跟踪指标的应用在“[误差调整动量](https://cssanalytics.wordpress.com/2014/07/30/error-adjusted-momentum/ "误差调整动量")”中讨论过。在上一篇文章中，许多问题和评论与加速度波动的具体计算（VOA）有关。答案是，这是一个通用概念，具体计算方法有很多种。但为了缩小范围，我将提出我认为最稳定的一种方式，并讨论如何进一步扩展这个概念。

**VOA= 平均值: | ln(pt/pt-1)- ln(pt-1/pt-2) |…….. | ln(pt-n/pt-n-1)|**

本质上，VOA 是每日对数收益的一阶差的绝对值的平均值。这里有一个电子表格图片，帮助澄清这个基本计算：

![accel 3](https://cssanalytics.files.wordpress.com/2014/12/accel-3.png)

这里有一个名为“**Forecast VOA**”的替代框架，它将今天与昨天的**VOA**变化纳入考虑，使得该指标的滞后性比原始**VOA**更小：

**预测 VOA（F-VOA）= VOA(t)+ k*(VOA(t)- VOA(t-1))**

其中“k”是一个在 0 和 1 之间的常数，可以手动选择或通过优化选择。滞后不需要是 1 天，而是可以选择任意数量的向后天数。常数 k 和滞后的数量可以作为独立或递归过程，类似于 EMA，先前解决的度量被反馈到下一个时间步中。在下面的示例中，我使用了 S&P500(SPY)上的“Forecast VOA”，滞后为 1 天，以及一个“k”值等于 1。我使用了一个 10 天的回溯期基线 VOA，并没有使用递归。目标 VOA 设置为 1%，其中头寸大小计算为目标%除以 VOA。为了与标准波动率头寸大小进行比较，我使用了 10 天的回溯期，并计算了 10 天 VOA 和 10 天波动率之间的 20 天滚动对冲比率，并将其乘以目标%以进行归一化。以下是结果：

![加速 5](https://cssanalytics.files.wordpress.com/2014/12/accel5.png)

![加速 6](https://cssanalytics.files.wordpress.com/2014/12/accel-6.png)

在收益和风险调整（夏普比）方面，预测的 VOA 和标准的 VOA 都优于使用标准波动率。读者会发现，标准的 VOA 通常在 S&P500 从短期到长期的一系列回溯期中优于使用标准波动率。然而，少于 10 天的短期度量通常太嘈杂，不能使用，因为它们包含了一阶差分。使用预测的 VOA 似乎优于 VOA，但需要注意的是，至少需要解决参数“k”来校准模型。更有雄心的公式将解决“k”和最佳滞后，并可能包含方程中的其他项。在这一点上，需要进一步研究其他工具，如一位读者建议的，但是使用类似 F-VOA 的框架可以允许适应以提高性能和跨市场一致性。VOA 框架是朝着寻找替代可能更好的波动率度量的方向迈出的一步。然而，还有一些非常复杂的计量经济学方法，如 GARCH 来预测波动性，强烈建议读者也去探索。
