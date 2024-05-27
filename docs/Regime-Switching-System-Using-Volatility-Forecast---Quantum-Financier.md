<!--yml

分类：未分类

date: 2024-05-18 14:03:03

-->

# Regime Switching System Using Volatility Forecast – Quantum Financier

> 来源：[`quantumfinancier.wordpress.com/2010/08/27/regime-switching-system-using-volatility-forecast/#0001-01-01`](https://quantumfinancier.wordpress.com/2010/08/27/regime-switching-system-using-volatility-forecast/#0001-01-01)

与昨天的文章思路一致，今天我们将探讨如何将我们昨天介绍的 GARCH 波动率模型融入其中，以创建一个切换策略。

博客圈经常讨论高波动性对日常均值回归（MR）有利，可参考 Michael 在 MarketSci 博客上发布的短期均值回归状态报告[这里](http://marketsci.wordpress.com/2010/08/01/the-new-state-of-short-term-mean-reversion-july-2010/)和 David 在 CSS Analytics 博客上发布的日常跟随均值回归系列[这里](http://cssanalytics.wordpress.com/2009/08/24/moderators-of-daily-follow-through-mr-volatility-part-1-of-3/)和[这里](http://cssanalytics.wordpress.com/2009/08/25/moderators-of-daily-follow-through-mr-implied-volatility-vs-historical-volatility/)。同时，低波动性环境通常是有利于趋势跟踪策略的；参考 Jez Liberty 的的趋势跟踪状态报告[这里](http://www.automated-trading-system.com/state-trend-following-ijuly/)。

考虑到这一点，由于我们希望最大化我们的回报，因此我们希望根据波动性环境交易适当的策略。使用波动率，我们可以动态地在 MR 和 TF 策略之间切换，以更好地适应当前市场范式。为此，我们可以使用 252 个交易日的回溯期对当前波动率进行百分位分类。结果系列在 0 和 1 之间波动，并使用 21 个交易日的[percentrankSMA](http://cssanalytics.wordpress.com/2010/05/19/percentrank-sma/)（由 David Varadi 开发）进行平滑，回溯期为 252 个交易日。现在我们有一个简化的波动率切换策略振荡器，读数大于 0.5 表示高波动性，小于 0.5 表示低波动性。

以下示例中，切换策略（RS）如下：如果振荡器大于 0.5，我们交易 MR 策略，当振荡器低于 0.5 阈值时，我们交易 TF 策略。MR 策略代理是 RSI2，TF 策略代理是 50-200 日移动平均线交叉，用于这个简单测试。下表显示了 SPY 的测试结果，包括仅 MR（红色）、仅 TF（蓝色）、买入持有（绿色）和 RS（黄色）的权益曲线。注意，在这个测试中，波动率的输入是收益的 21 日滚动标准差（即历史波动率）。

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/08/rsstrategy1.png)

RS 策略在过去 10 年中优于 MR 和 TF 策略。但是等一下，这篇文章是关于使用波动率预测进行状态转换，而不是历史波动率。很简单，要做到这一点，我们使用上篇文章中介绍的 GARCH 模型的结果来计算振荡器。现在我们有了使用波动率预测的 RS 策略，好消息是：它的表现更好！以下使用 GARCH 预测（金色）与使用历史波动率（灰色）的结果对比。

![RSstrategy2](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/08/rsstrategy2.png)

![RSstrategy - result](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/08/rsstrategy-result.png)

如前所述，在许多其他博客上，在策略中融入波动率预测似乎可以改善这种状态转换策略的结果。

量化金融师
