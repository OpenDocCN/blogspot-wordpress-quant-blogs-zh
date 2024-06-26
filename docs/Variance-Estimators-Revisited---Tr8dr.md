<!--yml

分类：未分类

日期：2024-05-18 15:37:34

-->

# 方差估计器再访 | Tr8dr

> 来源：[`tr8dr.wordpress.com/2009/11/17/variance-estimators-revisited/#0001-01-01`](https://tr8dr.wordpress.com/2009/11/17/variance-estimators-revisited/#0001-01-01)

我需要对我正在工作的策略进行合理准确的日内方差测量。 在我之前的一篇文章中，我指出虽然 GARCH(1,1)很好地拟合了日回报，但它对日内回报拟合得不好。 实际上，它拟合得如此之差，以至于无法得到非零的最大似然值。

对于日内 GARCH 模型的失败是多方面的。 日内（平方）回报表现出：

1.  随机大幅跳跃后急剧下降

1.  微观结构噪声

1.  回报中的明显缺口作为平滑的自回归过程

**Garch 再访**我决定重新审视 GARCH； 也许经过一些修改可以用作粗略的测量，而不是更复杂的模型。

日内数据中的“跳跃”在高斯误差模型中的概率接近 0。 为了解决这个问题，在 GARCH 模型中增加了一个组件来吸收跳跃冲击：

![图片 1](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-17.png)

新增的组件是**J**，它吸收了超过阈值的过量回报。 上面基本上说明跳跃对后续平方回报的预测价值没有（尽管这并不是严格观察到的情况）。 更有可能的是，跳跃应被视为一个主要独立于总体方差的随机过程。

阈值是通过启发式方法确定的：

![图片 1](img/picture-18.png)

利用上述公式，我能够校准到一个相对较高的似然值和 R²，样本值为 0.90，外部值为 0.85，即带有截断跳跃。

![图片 9](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-92.png)

**基于持续时间的方法**

对于基于布朗运动的进程，我们知道在时间间隔Δt 内的增量Δr 按如下比例缩放，并且一个暗示另一个：

![图片 3](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-37.png)

基本上这意味着我们可以估计Δr 在价格（回报）过程中实现的时间量。 Engel 和 Russell 开发了一个广受好评的价格持续时间模型，称为自回归条件持续时间模型（ACD）。 该模型用持续时间（或交替地用强度）来表示价格变动，但没有明确提供方差估计。

为了这个模型，让我们假设一个粒度常数 Δ**r**。然后让 **D**[t] 表示过程在 [t, t-1] 之间移动 Δ**r** 所需的有效时间跨度。这大约是 Δ**r** 除以回报的变化（大约）。例如，如果 Δ**r** 表示由 1 个点组成的回报，并且在 1 秒内看到了 3 个点的回报，那么 D[t] 将是 1/3。

在强度方面，我们可以将这个问题建模为：

![](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-43.png)

我们希望将方差转化为可以利用强度进行估计的形式。由于方差表示为回报的平方的期望值，我们可以从概率的角度来表述这个问题：

![](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-72.png)

我们可以使用泊松分布来模拟条件概率 p(k jumps | λ)，并计算跳跃到某个最大跳跃大小 m 的离散积分。

**处理跳跃**

从经验上看，跳跃似乎遵循与非跳跃价格变动不同的过程。为了解决这个问题，我增加了一个单独的过程来处理跳跃，由一个单一因素引导指数衰减。在计算期望值时，这两个过程会结合在一起：

![](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-82.png)

决定何时将回报视为跳跃 J 或标准回报 D（两者均作为持续时间）是一件复杂的事情。我们可以这样决定：

D = max (*价格持续时间对于[t-1,t]*, *跳跃阈值*)

J = max (*价格持续时间对于[t-1,t] – D, 0*)

或者决定将整个回报分类为跳跃或正常回报。

**季节性**

我们可能还想调整常数 **Dμ**，以便根据交易日的不同阶段调整不同水平。例如，开盘和收盘时，持续时间会很短（方差高）。这将需要构建交易日的季节性曲线。

在外汇市场中，不同的交易时段提供的流动性程度不同。流动性降低时，我们可能会看到价格动作很小，价格出现很大的（通常是暂时的）跳跃。这些时段的强度自相关性可能会有所不同，更不用说基本强度了。采用马尔可夫切换模型可能是适应不同市场条件的最佳方式。

**结果**

我现在正在实施这个方案。将看看它与修改后的 GARCH 过程相比如何。也可能研究跳跃过程的一些变体。
