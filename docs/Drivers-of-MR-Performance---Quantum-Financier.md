<!--yml

类别：未分类

日期：2024-05-18 14:04:59

-->

# MR 性能的驱动因素 - 量子金融家

> 来源：[`quantumfinancier.wordpress.com/2010/05/24/drivers-of-mr-performance/#0001-01-01`](https://quantumfinancier.wordpress.com/2010/05/24/drivers-of-mr-performance/#0001-01-01)

博客圈讨论的许多日常均值回归策略都是为股票指数 ETFs 或股票指数共同基金设计的。指数是由个别股票组成的集团，如果我们能确定哪些股票将驱动指数收益或在这种情况下，行为，我们可以调整策略以从指数的驱动因素所指示的主导市场范式中获利。

例如，如果影响指数最多的股票主要表现出均值回归行为，我们可以预期指数也会表现出相同的行为。趋势行为也适用于相同的结论。这里的重要一点是指数本身并不是一个实体；它们是为了反映某个部门/股票类型/区域等而制定的。为了说明这个概念，我使用了流行的无界 DV 2 执行了一个简单的测试。

我使用纳斯达克 100 及其相关的 ETF QQQQ 来执行此测试。首先，我需要一种定量确定市场驱动因素的方法。为此，我使用了加权的 r 平方。你们中的许多人都知道 r 平方是另一个名字：决定系数。该统计量提供了一系列由另一个系列预测的水平的指示（即拟合优度）。要获得它，你只需将相关系数提高到 2 的幂。对于这个测试，我只看了过去 21 天的 r 平方，并且是滚动的。然后，我查看了指数的每个个体组成部分的交易量与所有组成部分的总交易量之间的比例，然后用这种特定股票的交易量的比例加权 r 平方。

更严格的形式如下：

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/drivers-of-mr-formulas.png)

对于每只股票在每个时期 n 的计算后，我取加权 r 平方最高的前 10 只股票，并计算它们的 DV2 值，将其平均化，并根据 DV2 给出的信号交易 QQQQ（从 0 开始做多/做空）。以下结果比较了这种策略、买入并持有 QQQQ 和 QQQQ 数据上的 DV2。

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/drivers-of-mr.png)

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/drivers-of-mr-res1.png)

正如你所见，结果相当相似，并且符合预期，高度相关。它表明，在由 100 只股票组成的指数中，仅查看对收益影响较大的一组股票可以帮助确定指数本身的 MR 表现。

QF
