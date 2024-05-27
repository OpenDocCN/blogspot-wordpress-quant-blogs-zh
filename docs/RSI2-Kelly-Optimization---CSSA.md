<!--yml

分类：未分类

date: 2024-05-12 18:18:39

-->

# RSI2 凯利优化 | CSSA

> 来源：[`cssanalytics.wordpress.com/2010/09/14/rsi2-kelly-optimization/#0001-01-01`](https://cssanalytics.wordpress.com/2010/09/14/rsi2-kelly-optimization/#0001-01-01)

凯利最优分配可以扩展到策略，正如之前在非参数统计方面的文章所暗示的那样。在这种情况下，我们使用传统的皮尔逊协方差来展示分配模型对于策略分配是有用的。当前模型的输入回顾期为 3 年或 756 天。在这种情况下，分配是在持有标普 500 指数和在同一直指上使用 RSI2 50/50 系统之间进行的。该投资组合可以对模型组件进行多头或空头操作。在这种情况下，包含持有策略很重要，因为如果 RSI 策略无效，我们只需持有市场，从而降低表现不佳的机会（即持有）。这是一个微妙的观点，因为对于给定市场来说，有效的策略可能根本不存在，因此在一组较差的策略中分配将大大增加表现不佳的可能性，这对于许多经理来说确实会影响资产管理规模（AUM）。正如你所见，分配模型的表现相当一致，几乎每年都优于持有。本周稍晚将介绍一个更复杂的分配模型。

![](https://cssanalytics.files.wordpress.com/2010/09/rsi2.png)

![](https://cssanalytics.files.wordpress.com/2010/09/rsi2_level2_long-only_756dcagrcov_table.png)
