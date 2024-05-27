<!--yml

类别：未分类

日期：2024-05-12 18:20:07

-->

# 随机制度思考 | CSSA

> 来源：[`cssanalytics.wordpress.com/2010/08/04/random-regime-musings/#0001-01-01`](https://cssanalytics.wordpress.com/2010/08/04/random-regime-musings/#0001-01-01)

现在众所周知，历史波动性是均值回归表现的重要调节变量。这只是常识，并且得到了研究的有力支持。另一个很好的总结（和出色的可视化）是由**杰夫·皮切**完成的，他来自酷炫的新站点**ETF Prophet  [`etfprophet.com/relative-volatility-comparative-mean-reversion-strategy-performance/`](http://etfprophet.com/relative-volatility-comparative-mean-reversion-strategy-performance/)**，以前是 Market Rewind 的名人。在这篇文章中，杰夫展示了如何通过对 100 天历史波动性进行 3 年相对排名，对基本的 RSI2 策略产生了重大影响。另一系列帖子以更详细和简单的方式解释了事情，易于理解，由**Woodshedder**完成 [`ibankcoin.com/woodshedderblog/2010/07/19/part-4-the-secret-ingredient/`](http://ibankcoin.com/woodshedderblog/2010/07/19/part-4-the-secret-ingredient/)。使用较短或更复杂的波动性转换/测量方式可以进一步提高均值回归收益的分离度。但这不是重点——事实上，重点是我们以某种方式使用*历史波动性*来确定我们现在如何进行交易。

现在我要连接一些点：

事实 1：我们可以通过将读数分成不同的四分位数或五分位数来测量 30 天波动性对简单均值回归策略的历史影响。这些可以代表不同的波动率制度。

事实 2：使用这些制度信息，我们实际上可以通过调整赌注大小或敞口来改善样本外策略表现。***然而，对于衡量当前历史波动性的指标，存在固有的滞后***。

事实 3：波动性——比如 30 天波动性——可以使用甚至简单的投影模型远比市场价格更可靠地预测。在学术界，使用波动率预测模型（EGARCH 等）已经得到很好的确认，并被认为是相当稳健的。

结论：使用预测或投影波动性将大大有助于基于制度的策略敞口模型。换句话说，***通过使用前瞻性估计，我们可以更快地响应波动性的变化，以及它们将如何影响我们的均值回归策略。***
