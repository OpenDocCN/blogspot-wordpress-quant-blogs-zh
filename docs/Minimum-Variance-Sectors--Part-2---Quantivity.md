<!--yml

类别：未分类

日期：2024-05-18 13:51:37

-->

# 最小方差行业：第二部分 | Quantivity

> 来源：[`quantivity.wordpress.com/2011/04/22/minimum-variance-sector-rotation-part-2/#0001-01-01`](https://quantivity.wordpress.com/2011/04/22/minimum-variance-sector-rotation-part-2/#0001-01-01)

继续分析 sectors 的旋转与[最小方差投资组合](https://quantivity.wordpress.com/2011/04/17/minimum-variance-portfolios/)，John Hall 询问了在[前一篇帖子](https://quantivity.wordpress.com/2011/04/20/minimum-variance-sector-rotation/)所描述的时间段之外，最小方差行业旋转的表现。这篇文章扩展了分析，考虑从美国行业 ETF 的*创立之初*（大约 1998 年底）开始的时间段，揭示了几处意想不到的乐趣。

1999-2010 年期间包括多种市场价格机制：两个泡沫，混合上升/下降趋势，以及充足的均值回归。从 MVP 行业权重开始最小方差行业旋转分析，这些权重意外地很有趣：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/04/annual-mv-sector-weights-1999.png)

特别是，2000-2002 年揭示了必需消费品行业权重的*显著*变化：从 20%增加到 100%。进一步研究 2001-2002 年的权重过渡，差异为(*即* `round(annualWeights[4,] - annualWeights[3,],3)`)：

| XLB | XLE | XLF | XLK | XLI | XLP | XLU | XLV | XLY |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0.011 | -0.042 | -0.155 | -0.112 | 0.159 | 0.446 | -0.303 | -0.012 | 0.008 |

因此，必需消费品的增加是以公用事业(-30.3%)、金融(-15.5%)和科技(-11.2%)的显著减少为代价的。从经典的行业旋转神话来看：金融和科技是“增长”，而公用事业是“防御”。科技减少可以理解，因为泡沫破裂；金融减少不太清楚，或许可以解释为它是“增长”。对于公用事业的大幅减少，没有立即的经济解释，除了 2002 年与科技泡沫低谷相一致这一明显事实。值得深思。

接下来，对前 5 个主导成分的年 PCA 分解，证实了市场错位与来自*市场成分*的方差比例增加之间的关系：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/04/longitudinal-pca-decomp-1999.png)

接下来，考虑在这个延长的时间段内这些权重产生的每日盈亏：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/04/mvp-pl-19992.png)

这种策略在整个期间内都超越了基准，最多超出 80%。为了更好地理解这种超越的时空动态，定义“alpha”为策略和 SPY 回报之间的*利差*（即`alpha <- cumsum(dailyPnL[2:length(dailyPnL)]) - cumsum(diff(log(coredata(spy))))`）。以下是在该期间 alpha 时间序列的说明：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/04/min-var-alpha-19992.png)

这强烈地暗示了 alpha 生成可能与市场价格波动的下降成反比，这与*先验*直觉相符，即 MVP 旨在最小化方差。为了进一步调查，请考虑将这两个时间序列关系叠加的图表：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/04/min-var-alpha-diff2.png)

这证实了这两个系列都是强烈的**异方差性**（毫不奇怪），并且 variance 变化之间有强烈的时空同时性。似乎存在强烈的相关性，但尚不清楚时间序列是正相关还是负相关。为了调查方向性，请考虑以下年度皮尔逊相关系数，该系数衡量的是 alpha 和 SPY 的第一差分：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/04/alpha-spy-correlation.png)

这确实证实了*alpha 变化与相应 SPY 变化之间存在强烈反比关系*（注意 y 轴是*负值*）。考虑到寻找与基准资产类别之间的负相关性，这确实很有趣。

将前面的负相关性与美国行业（由同一行业 ETF 衡量）的年均相关性进行比较，体现了在困境下的典型强正相关：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/04/mean-sector-correlation.png)

总之，前面的分析确实表明最小方差组合实现了它们的目标，即在“好”（上涨）方差或缓和方差期间同时削减“坏”（下跌）方差而不减少 alpha。

* * *

想要在 R 中跟进的读者，本篇文章依赖于上述内容以及以下额外逻辑：

```

# plot annual alpha-spy correlation
plot(array(sapply(annualNames, function(yr) { cor(dalpha[yr], dspy[yr])})), type='l', xaxt="n", xlab="", ylab="Correlation", main="Alpha-SPY First Difference Correlation")
axis(1, 2:nrow(annualNames), annualNames[2:length(annualNames)])

# plot annual sector correlation
plot(sapply(annualNames, function(yr) { mean(cor(usRets[yr])) } ), type='l', xlab="", ylab="Correlation", xaxt="n", main="Mean Sector Correlation")
axis(1, 1:nrow(annualNames), annualNames)

```
