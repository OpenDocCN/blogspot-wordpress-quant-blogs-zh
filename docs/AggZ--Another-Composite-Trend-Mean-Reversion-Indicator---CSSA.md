<!--yml

category: 未分类

date: 2024-05-12 18:33:50

-->

# AggZ: 另一个综合趋势/均值回归指标 | CSSA

> 来源：[`cssanalytics.wordpress.com/2010/03/19/aggz-another-composite-trendmean-reversion-indicator/#0001-01-01`](https://cssanalytics.wordpress.com/2010/03/19/aggz-another-composite-trendmean-reversion-indicator/#0001-01-01)

这是一个非常简单的指标，拥有数十种应用。与 AggM 类似，AggZ 是一个综合趋势和均值回归指标。这两个概念旨在将长期趋势测度与短期均值回归测度相结合，以便您可以拥有一个既适合长期又适合短期交易的指标。在 SPY 上，AggZ 使用股息调整数据，在过去的 2000 个条柱上实现了 20%的年复合增长率（CAGR）。计算非常简单：

AggZ= (-1x( 10-day z-score)+(200-day z-score))/2

Z 分数 = (收盘价-收盘价在过去 n 个周期内的简单移动平均)/(收盘价在过去 n 个周期内的标准差)

基本策略是在 0 以上购买，在 0 以下卖出。

用户可以尝试不同的 Z 长度以及买入/卖出点。顺便说一句，***期待 Amibroker 的 DV 指标下周发布 - 我们终于大功告成了！***更多信息即将发布。

![](https://cssanalytics.files.wordpress.com/2010/03/aggz_spy1.png)
