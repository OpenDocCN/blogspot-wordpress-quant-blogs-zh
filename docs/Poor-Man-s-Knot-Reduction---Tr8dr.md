<!--yml

类别：未分类

日期：2024-05-18 15:34:43

-->

# Poor Man’s Knot Reduction | Tr8dr

> 来源：[`tr8dr.wordpress.com/2010/01/18/poor-mans-function-approximator/#0001-01-01`](https://tr8dr.wordpress.com/2010/01/18/poor-mans-function-approximator/#0001-01-01)

在 R、SAS 等包中有许多很好的**单位根**测试实现。出于各种原因，我需要用 Java 实现这个。最著名的这类测试是 augmented Dickey Fuller test。这通常用于确定一个过程是非平稳的还是在支持平稳性方面被拒绝。

粗略地说，说一个过程是平稳的意味着它的所有矩在很大程度上是时间不变的。例如，平稳过程的均值和方差（很大程度上）在时间上是恒定的。

我们知道 AR(1)过程的 AR 系数α=1 时，其方差是无限的，随时间增长。这可以通过计算其方差来看：

![](https://tr8dr.wordpress.com/wp-content/uploads/2010/01/unbounded.png)

因此，ADF 测试测试的是给定系列作为 AR(p)过程表达时具有 1（即单位根）的系数。ADF 在原始 Dickey Fuller 测试基础上扩展了额外的 AR 滞后：

![](https://tr8dr.wordpress.com/wp-content/uploads/2010/01/adf.png)

零假设是β=0（非平稳过程），而备择假设（可能是平稳的）则相反。注意，在这个差分方程中β=0 与非差分 AR(1)方程中的α=1 是等价的。

在假设测试中，样本（即观察值与零假设值的差异）通常遵循学生 t 分布。在 Dickey Fuller 测试的情况下，分布不是学生 t 分布，因此这是一个问题。为了计算 ADF 假设的 p 值，必须查阅特殊的 Dickey-Fuller 表，因为据我所知，没有已知的封闭形式方法来计算这个。

我们知道 p 值是获取的样本结果至少与我们样本中获得的远离假设值一样极端的概率。这涉及计算：

![](https://tr8dr.wordpress.com/wp-content/uploads/2010/01/pvalue.png)

然后，为了确定 ADF 的 p 值，我们需要确定围绕零假设β=0 的值分布。表提供了测试值和累积概率的预计算映射。

**问题

Dickey-Fuller 表很稀疏，特别是在尾部。对于我的问题，我感兴趣的是许多不同序列的相对“平稳性”。为此，我需要用自己的蒙特卡洛模拟计算 Dickey-Fuller pdf.**

以下是 Dickey-Fuller 假设的 pdf 的一个配置（由蒙特卡洛模拟产生）：

![](https://tr8dr.wordpress.com/wp-content/uploads/2010/01/dist.png)

当然，每次评估 ADF 测试时都不实用蒙塔卡洛模拟。MC 模拟的结果生成了一系列（x,y）点的高分辨率密度函数。我可以为多种配置生成分布，并存储一个非常大的 3D 函数值表，但这是不切实际的且不必要的。

我开始思考分布的近似函数。除了通过试错找到分布的功能形式外，一种通用的自动化方法是使用样条。自然样条将适合函数并且是分段连续的。

然而，样条并不会降低问题的维度。自然样条需要完整的节点集合来重构函数。然后我开始思考节点减少技术。节点减少的想法是：在某种（小）误差范围内再现目标函数所需的最小节点集合。所以如果我的函数目前有 2000（x,y）点，也许我可以将其减少到~10 个点？

已经有很多关于这个主题的论文，通常涉及非常复杂的算法。因为我想保持这个简单，决定提出一个用于节点减少的“穷人算法”。

**算法**

算法从由 2 个端点组成的样条开始，逐渐在特定位置添加节点，迭代地减少“简化样条”与目标函数之间的误差。新节点是基于目标函数的最大距离选择的。**

**算法不能保证是最优的，因为它可能有比最小的再现集合更多的节点点。然而，它非常快，并且取决于函数，通常接近最优。算法如下：**

1.  从 2 个点（开始和结束点）的样条开始

1.  在循环中，当 R² < (1 – eps) 时继续循环。

    1.  在与目标函数距离最远的点添加节点

    1.  计算新的样条和 R² 拟合度量

1.  在循环结束时，节点的集合现在在 epsilon 范围内与函数匹配

采用更好的基函数（比 Hermite 三次样条）以及调整张力，可以增强这种方法的 effectiveness。

这是一个将 epsilon = 1e-8 的函数示例。我已经将其减速到每秒 1 次迭代，以便您可以看到它是如何工作的。在实际中，这涉及到几微秒：

[`www.youtube.com/embed/bu-tYr4onJc?version=3&rel=1&showsearch=0&showinfo=1&iv_load_policy=1&fs=1&hl=en&autohide=2&wmode=transparent`](https://www.youtube.com/embed/bu-tYr4onJc?version=3&rel=1&showsearch=0&showinfo=1&iv_load_policy=1&fs=1&hl=en&autohide=2&wmode=transparent)

VIDEO
