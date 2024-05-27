<!--yml

category: 未分类

日期：2024 年 05 月 18 日 14:04:13

-->

# 使用 GARCH(1,1)进行波动率预测- 量子金融家

> 来源：[`quantumfinancier.wordpress.com/2010/08/26/volatility-forecasting-using-garch11/#0001-01-01`](https://quantumfinancier.wordpress.com/2010/08/26/volatility-forecasting-using-garch11/#0001-01-01)

在继续当前一系列的帖子时，我正在预测波动率的点。有几种方法可以做到这一点；这个话题在金融领域进行了大量研究。有各种不同的模型可以模拟波动率，涵盖了从简单到复杂的整个范围。我将使用我认为是最流行的之一：GARCH(1,1)。不过，我认为这并不是最好的模型，但我确实认为它的简单性使其非常吸引人。对于更复杂的量化分析人群来说，在 GARCH 家族中，EGARCH 似乎比其他模型更好地预测市场波动率。我不打算详细介绍 GARCH 过程（即这不是一篇介绍性的文章），如果你想了解更多，请在评论部分告诉我。

对于自 2000 年以来的 SPY 股票，这是一个 GARCH(1,1)模型的情况，与 21 天标准偏差一起绘制在底部的残差。结果是使用 R 的 tseries 和 quantmod 库创建的。

![")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/08/garch11.png)

在显著性方面，该模型明显地过滤了 ARCH 效应，条件正态性假设似乎没有被违反（使用 Jarque Bera 和 Box-Ljung 测试）。不管是照本宣科的测试，还是用眼睛观察图表，我们看到该模型在预测 SPY 的波动率方面相当不错。现在我们已经建立了模型，下一篇文章应该是如何在波动率被剥离与实际波动率的相关性后使用类似的模型，以查看我们是否可以改善交易结果，特别是我们的制度切换策略。

QF
