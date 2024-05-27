<!--yml

分类：未分类

日期：2024-05-12 18:39:30

-->

# SMA ROC(1)：比基于价格的简单移动平均更好的趋势测量方法 | CSSA

> 来源：[`cssanalytics.wordpress.com/2009/12/21/sma-roc1-a-better-trend-measurement-than-price-based-moving-averages/#0001-01-01`](https://cssanalytics.wordpress.com/2009/12/21/sma-roc1-a-better-trend-measurement-than-price-based-moving-averages/#0001-01-01)

***注意：以下策略使用 yahoo finance 数据进行多/空交易。对于 sma roc(1)，当 sma roc(1)大于零时触发多头信号，当它小于零时触发空头信号。SMA 策略使用标准方法进行交易，即多头>sma，空头<sma。***

有时候，简单地对其他方法中的固有缺陷进行改进，真的可以带来很大的不同。简单移动平均（SMA）或基于价格的简单移动平均的主要问题之一是，它受到历史复利的影响，并且对价格变动反应迟钝。当价格或趋势突然变化时，这种滞后和扭曲可能会导致一些严重的高低波动问题。动量或简单回报是速度的度量，它有更快反应价格变化的好处。这种提高的敏感性和准确性在捕捉价格波动方面非常有价值。这也是历史波动率计算中考虑价格回报的标准差而不是像布林带那样的价格平均值除以标准差的原因。这个概念的最简单和最基本的应用是取价格的 SMA 或 1 日 ROC（变化率）。使用这种方法可以显著提高回报并减少回撤。以下是 SPY（标普 500）的 20 日和 200 日价格 SMA 与 sma of ROC(1)的图表。正如他们所说，细节决定成败！

![](https://cssanalytics.files.wordpress.com/2009/12/1031.png)
