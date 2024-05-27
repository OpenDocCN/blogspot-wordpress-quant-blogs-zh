<!--yml

类别：未分类

日期：2024-05-12 19:24:46

-->

# 量化交易：通过 XLE 进行指数套利

> 来源：[`epchan.blogspot.com/2007/02/in-looking-for-pairs-of-financial.html#0001-01-01`](http://epchan.blogspot.com/2007/02/in-looking-for-pairs-of-financial.html#0001-01-01)

在寻找可以进行对冲交易的金融工具对时，我们不必局限于自然界中出现的对。我们通常可以构建自己的股票篮子来对抗一个指数（或代表这个指数的 ETF）。实际上，这样的对通常比任何股票或 ETF 对显示出更好的协同整合特性。我之前在

[文章](http://epchan.blogspot.com/2007/02/mr_05.html "文章")中有解释

，具体方法在我的

【订阅文章】(http://epchan.com/subscriptions.html "订阅文章")

提到了这个指数套利的想法。我尝试了这个策略在我最喜欢的行业 ETF：能源 SPDR XLE 上。

XLE 由大约 33 只股票组成（截至 2007 年 2 月 16 日）。我们的目标是挑选出这些股票中的一些小集合来形成一个篮子。我们根据它们与 XLE 的协同整合程度来挑选它们。这个子集应该有多大？数字越高，这个篮子与 XLE 的协同整合程度越高，但利润越低。（如果你包括 XLE 中的所有股票在这个篮子中，那么这个篮子与 XLE 的协同整合程度完美，但将没有交易机会！）数字越低，特定风险和回报也越高。因此，选择多少股票更多的是基于个人的风险回报偏好，而不是任何科学标准。我选择了一个包含 10 只股票的篮子。我发现自 2001 年 5 月 22 日以来，这个篮子与 XLE 的协同整合概率超过了 99%。

[半衰期](http://epchan.blogspot.com/2007/01/what-is-your-stop-loss-strategy.html "半衰期")

对于平均回归，大约是 20 天，这意味着你最多只能持有四分之一的仓位。（我的规则是在价差没有回归到一半生命周期的三倍时退出。）如果你在 z-score 约为±2 时进入仓位，你可以在大约$58,000 的一边投资中预期获得大约$2,000 的利润。这意味着每笔交易的回报率约为 3%。当然，你也可以通过使用期权来实现 XLE 仓位来提高这个回报。

顺带一提，如果你使用 Interactive Brokers，你可以使用他们的篮子交易器轻松交易一个完整的股票篮子。

我创建了一个在线电子表格，实时显示这个价差在

[订阅区](http://epchan.com/subscriptions.html "订阅区")

。（这个包含 10 只股票的篮子的详细组成也在那里。）请注意，在理论上，每次 XLE 改变组成时，我们都需要重新计算我们的篮子组成。但幸运的是，XLE 的组成变化不大，也不经常变化，所以我最多一个月更新一次我的篮子。

![图片](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj2YZcqsZKHxyHLMFr1cZNaaXS3Lb8pawzzeoqrRZxIv2G9jdfaUsoZjmDHG81UgAP7_Nac1TWISQ75MXNFgQA_8UckLfBKbeZCplO0AtybzYwru7oBV_WiLW7st1JwBtALJGca0A/s1600-h/XLE.bmp)
