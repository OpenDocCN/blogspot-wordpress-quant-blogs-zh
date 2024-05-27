<!--yml

类别：未分类

日期：2024-05-12 18:16:26

-->

# 一种新的趋势指标：MSR | CSSA

> 来源：[`cssanalytics.wordpress.com/2010/10/27/a-new-trend-indicator-msr/#0001-01-01`](https://cssanalytics.wordpress.com/2010/10/27/a-new-trend-indicator-msr/#0001-01-01)

虽然我的研究重点通常转向了将多指标/多变量模型结合起来的技术，但最终我还是依赖于各种单一指标输入进行这种方法。 因此，捕捉稍微不同的东西或通过将一个概念压缩成一个数字来减少模型的复杂性的指标仍然非常可取。 Quantum Financier 的一篇很好的文章强调了这些问题的重要性：[`quantumfinancier.wordpress.com/2010/10/22/considerations-in-systemindicator-design/`](http://quantumfinancier.wordpress.com/2010/10/22/considerations-in-systemindicator-design/) 。

在这种情况下，我正在寻找一个捕捉短到中期时间范围内的典型或中间价格的支撑和阻力指标。 我还想要一些可以归一化的东西，这样我就可以避免具有二进制规则或特定的入场和出场水平的不灵活性。 这是我想出的一个非常简单的东西，在标准普尔 500 指数（SPY）上表现良好，年复合增长率接近 10%，这对于一个短期指标来说是令人印象深刻的。

**MSR**=（10 天（H、L、C）的中位数 - 20 天 MAX（H、L、C））/（20 天 MAX（H、L、C））

然后计算 MSR 的 252 天百分位排名或百分位排名

初始化的多头交易>.5

初始化的空头交易<.5
