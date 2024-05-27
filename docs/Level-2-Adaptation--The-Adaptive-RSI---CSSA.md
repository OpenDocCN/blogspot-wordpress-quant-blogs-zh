<!--yml

category: 未分类

date: 2024-05-12 18:31:48

-->

# Level 2 适应性：适应性 RSI | CSSA

> 来源：[`cssanalytics.wordpress.com/2010/04/09/level-2-adaptation-the-adaptive-rsi/#0001-01-01`](https://cssanalytics.wordpress.com/2010/04/09/level-2-adaptation-the-adaptive-rsi/#0001-01-01)

每当我发现自己突然在谈论一级或二级技术时，我总会想起 Jeff Pietsch of **[ETF Rewind](http://etfrewind.blogspot.com/)**，他是编程**DV 指标 Excel 插件**背后的真正巫师——此外，他还是一个非常聪明的人。一个人只能想象处理我和我繁琐的计算所花费的时间和精力（以及头痛！）。（我们两个都可能是个大麻烦！）但是他设法把一切都精确到小数点后一位。

昨天我们对“分形 RSI”进行了偷窥，这是一种自适应的 RSI 变体，动态地在 2 到 30 天之间变化，以考虑市场波动的程度。 “分形 RSI”是一个一级自适应指标：它调整市场状况，但并没有自我意识。二级适应性代表指标理解其盈利来源组成部分的能力。请注意，这并不是优化，也不是使用定时机制交易 equity curve。像适应性 RSI（DVAR）这样的二级适配器，如有必要，会在趋势和逆趋势之间以及从 2 到最大 30 的参数长度之间调整权重。它观察盈利分布以调整指标输出。它无法像分形 RSI 那样处理当前市场状况的调整。然而，它可以更好地理解给定市场的行为。下面是一个有趣的测试，我们将 DVAR 回测到 1974 年的纳斯达克综合指数和标普 500 指数。我们让 DVAR 生成买入和卖出信号，简单地交易总回报最高的市场。没有使用定时机制交易 equity curve。**35 年回测的结果是无摩擦的复合回报率为 33.68%。** 只有两年是亏损的：2003 年和 2004 年，对于那些做了很多测试的人来说——在那个时期有很多表现良好的系统，*包括分形 RSI！* 这让我想到我的最后一点，那就是使用多种适应性类型和/或指标是实现一致性的真正圣杯——但二级适应性总是有帮助的 :o) [![DVAR](https://cssanalytics.files.wordpress.com/2010/04/007.png)](https://cssanalytics.files.wordpress.com/2010/04/007.png)

![DVAR 年度表现](https://cssanalytics.files.wordpress.com/2010/04/0081.png)

![DV 插件控制面板](https://cssanalytics.files.wordpress.com/2010/04/0091.png)
