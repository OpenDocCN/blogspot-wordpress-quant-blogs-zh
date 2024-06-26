<!--yml

类别：未分类

日期：2024-05-12 18:50:50

-->

# SMR-针对熊市的情绪和均值回归交易系统 | CSSA

> 来源：[`cssanalytics.wordpress.com/2009/08/18/smr-a-sentiment-and-mean-reversion-trading-system-for-bear-markets/#0001-01-01`](https://cssanalytics.wordpress.com/2009/08/18/smr-a-sentiment-and-mean-reversion-trading-system-for-bear-markets/#0001-01-01)

在熊市中持仓过久可能会是一个非常令人恐惧的提议。RSI 2 或 DV2 的极端读数在我们俯瞰深渊时并不能给我们带来安慰。我希望设计一个系统，它集成了各种因素，以最大化成功的概率，并最小化极端损失的概率。我还希望这个系统在市场中的时间尽可能短。我将这个系统称为“SMR”，因为它结合了情绪指标和均值回归指标。在此情况下，我将熊市定义为 SPY 低于其 252 天的平均收盘价。以下是一些系统输入：

均值回归指标

1) 无限制 DV2

2) 每日跟进

3) DVS（拉伸指标）

情绪指标

1) VIX-波动指数

2) 通过加拿大中央基金（CEF）投资黄金和白银——真正的黄金爱好者的最爱

**SMR** 系统规则：

如果是熊市：SPY < 252 天的平均收盘价

1) DV2 无限制小于零

2) 市场低于昨天的收盘价

3) DVS 小于 50 百分位

4) 从昨天的收盘价以来 SPY 表现优于 CEF

5) VIX 高于昨天的收盘价

如果满足所有这些规则，则在收盘时买入 SPY，当条件不再满足时卖出（通常交易持续 1 天）。以下是过去 2 年的结果：

| **SMR 系统 2007 年 8 月 23 日至今** |   |
| --- | --- |
|   |
|   | 平均收益 | 正确百分比 | 最大损失 | 最大收益 | 交易次数 |   |
| 买入信号 | 1.7% | 80.2% | -4.40% | 14.50% | 25 |   |
|   |   |   |   |   |   |   |
| **SMR 系统 2007 年 8 月 23 日至今绩效总结** |   |
|   |
|   | 年化复合增长率 | 标准差 | 夏普比率 | R 平方 | DVR（夏普率 xR 平方） |   |
| 买入信号 | 22.0% | 13.4% | 1.59 | 88% | 1.40 |   |

系统表现非常好，年化复合收益率为 22%，权益曲线非常平滑，R 平方为 88%。平均持仓时间不到 1.1 天，最大损失仅为-4.4%。只有两种连续触发的交易，而且都是赢的。
