<!--yml

分类：未分类

日期：2024-05-12 18:51:47

-->

# Normalizing Bollinger Bands Using DV Bands (part 1) | CSSA

> 来源：[`cssanalytics.wordpress.com/2009/08/05/normalizing-bollinger-bands-using-dv-bands-part-1/#0001-01-01`](https://cssanalytics.wordpress.com/2009/08/05/normalizing-bollinger-bands-using-dv-bands-part-1/#0001-01-01)

*大多数人错过了第二部分的内容，你可以在这里找到：* [`cssanalytics.wordpress.com/2009/08/06/`](https://cssanalytics.wordpress.com/2009/08/06/)part-2-improvi…-intraday-data/

设计布林带的主要推动力在于寻找一种能够准确包含给定证券大多数价格波动的方法。将标准设置为 20 天平均值，上下 2 个标准差，如果价格呈正态分布，理论上应该能包含 95%的价格。在约翰·布林格的书籍《布林格谈布林带》中提到，使用默认设置，测试价格实际上有 89%的时间被包含在布林带中。

在我的工作中一个关键的洞见是，使用经验分布对指标甚至股票排名进行标准化。我决定研究一下这种方法如何应用于布林带——这是交易员非常流行的一个指标。我选择测试 SPY 从 1995 年以来的数据。我将布林带与 DV 带进行比较，以确定该过程是否增加了统计价值。DV 带就是通过使用 252 天回溯的 PERCENTRANK 函数对当前 z 分数进行排名后标准化得到的布林带。DV 带和布林带都设置为 20 和 2，其中 20 是价格的 20 天平均值，±2 个标准差分别表示上轨和下轨。

首先，我运行了一个测试，看看实际上有多少价格在两种方法下落在了两个布林带之间：

|  | 实际价格下跌百分比 | 历史 |
| --- | --- | --- |
|   |  上下轨之间的误差 |  |
| 布林带 (20,2) | **91%** | **-4%** |
| DV Bands (20,2) | **95%** | **0%** |

正如你所看到的，布林带只包含了 91%的历史价格，这比如果值呈正态分布预期的要少 4%。相比之下，DV 带包含了 95%的历史价格——这正是我们所预期的，因为这些带子不假设价格呈正态分布，而是随着股票随时间演化的经验分布进行适应。那么超出样本呢？如果今天它们被包含在布林带中，那么今天它们包含在布林带中的价格百分比是多少？以下是结果：

|  | 下一交易日价格下跌百分比 | 预测 |
| --- | --- | --- |
|  |  上下轨之间的误差 |  |
| 布林带 (20,2) | **89%** | **-6%** |
| DV Bands (20,2) | **91%** | **-4%** |
|  |  |  |

| 如果今天的价格在上限和下限之间，样本外，我们还可以看到预测误差的改善。请注意，如果你使用更长的时间回溯期（percentrank），比如 4 年或 5 年，性能改善甚至更多。还有方法可以进一步改善这一点，比如使用不同历史值的 ADX 以及最后 20 天内的历史带宽来训练带宽。推测当带宽紧缩且 ADX 低但上升时，违反带宽的情况会更为频繁。同时使用 ATR 带宽 likely also add 额外的信息，因为它们与布林带宽不完全相关，因为它们包含日内数据。现在让我们看看这些改进对交易的影响：

|    | 第二天平均回报如果**低于**平均值   |

|    | 并且在上限和下限之间   |

| 布林带宽（20,2）   | **0.016%**   |

| DV 带宽（20,2）   | **0.0250%**   |

|    |    |

|    | 如果**高于**平均值，第二天返回   |

|    | 并且在上限和下限之间   |

| 布林带宽（20,2）   | **-0.004%**   |

| DV 带宽（20,2）   | **-0.012%**   |

平均每日回报在使用 DV 带宽时低于平均值购买相比布林带宽时高出 50%以上。平均每日回报在使用 DV 带宽时高于平均值购买相比布林带宽时低 200%。对交易员来说，这种影响实际上相当大。结果在不同带宽组合之间相当一致。证据似乎清楚地表明，标准化可以提高布林带宽的实用性。应用范围超越简单的均值回归策略，对期权交易员的影响可能最大。可以利用这些结果推导出一个新期权公式，以更准确地表示公平价格。在未来的研究（第二部分）中，我将展示更广泛的结果，并检查在不同资产类别之间鲁棒性。   |    |
