<!--yml

类别：未分类

日期：2024-05-18 14:04:51

-->

# 不同市场中的波动性自相关性 - Quantum Financier

> 来源：[`quantumfinancier.wordpress.com/2010/05/27/volatility-autocorrelation-in-different-markets/#0001-01-01`](https://quantumfinancier.wordpress.com/2010/05/27/volatility-autocorrelation-in-different-markets/#0001-01-01)

有关自相关性介绍，请参阅此前的文章：[First Order Autocorrelation as a Moderator of Daily MR](https://quantumfinancier.wordpress.com/2010/05/07/first-order-autocorrelation-as-a-moderator-of-daily-mr/)。

在上一篇文章中，我研究了自相关性如何指示 MR 表现，在本文中，我观察了另一个每日跟踪的调节者的自相关性；波动性。直觉上，波动性高度自相关是有道理的。VIX 飙升就是一个很好的例子。让我们看看在牛市/熊市期间波动性的自相关性表现如何，这是由 200/50 天移动平均线交叉定义的。

对于这个测试，我查看了 SPY 收益率 21 天滚动标准差的一阶到五阶自相关性，将它们分成百分位数（使用 252 天的回看期的百分位数函数），并观察了百分位数的平均值和标准差。

在开始测试之前，我认为收益率的波动性具有很高的自相关性。然而，我认为牛市和熊市之间会有更大的差异。下表中需要注意的一点是，当 50 天移动平均线大于 200 天移动平均线时，所有阶的自相关性平均值都更大。标准差也是同样的观察结果。

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/volatility-autocorrelation-in-different-markets-results.png)

就交易而言，这些信息本身并没有直接价值，但它用数字说明了一个明确定义的市场机制。我们知道，波动性比收益更容易预测，而自相关性的水平很大程度上负责这一事实。我们还知道，每日均值回归策略在高波动性时期表现更好。因此，我们可以将波动性自相关性用作我们策略适用性的指标。例如，在波动性高且自相关性高的高波动性期间，我们可以期待我们的策略表现良好，反之亦然，如果我们改变了条件。关于波动性可预测性及其在交易中的应用的非常有趣的阅读，我推荐托尼·库珀(Tony Cooper)的这篇最近赢得 NAAIM 2010 瓦格纳奖的文章。[`naaim.org/files/2010/1st_Place_Tony_Cooper_abstract.pdf`](http://naaim.org/files/2010/1st_Place_Tony_Cooper_abstract.pdf)

QF
