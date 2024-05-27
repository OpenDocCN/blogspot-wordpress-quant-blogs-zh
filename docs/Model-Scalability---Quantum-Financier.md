<!--yml

category: 未分类

date: 2024-05-18 14:0-39

-->

# Model Scalability – Quantum Financier

> 来源：[`quantumfinancier.wordpress.com/2011/02/15/models-scalability/#0001-01-01`](https://quantumfinancier.wordpress.com/2011/02/15/models-scalability/#0001-01-01)

When designing a model, an aspect that I often overlook is scalability. First a definition from Investopedia: “A characteristic of a system，model or function that describes its capability to cope and perform under an increased or expanding workload. A system that scales well will be able to maintain or even increase its level of performance or efficiency when tested by larger operational demands.”

Now most of you probably wonder why I would overlook such a crucial aspect of model building. The reason is very simple; I never had to. Most of the models I design are for my personal trading and since I don’t have millions of dollar in capital to trade (yet!), the scalability requirements are very insignificant. Most of my trading is on the mini futures and I only trade a few contracts per symbol. Keeping this in mind, I don’t have to worry too much about slippage when I place my orders since the effect of the order book are negligible. However， chances are I am not going to design models solely for my personal trading during my career.

对对冲基金而言，可扩展性的要求实际上是非常不同的。例如，想象一下在一个单一的符号上进行高交易量的策略，为了说明方便，我们考虑一个 RSI2 策略。这是一个非常短期的策略，对于一个日终策略来说，交易量相对较高。现在用 50k 来交易这个策略是可行的（不是最优的，但也不算太差），现在想象一下用 100mm 来在单一符号上交易 RSI2 信号；这是非常不切实际的。想想滑点会对策略产生多大的影响。在撰写本文时，SPY 开盘价为 133.02，交易 100mm 最终会在开盘报价时大约是 751,654 股。承认吧，我没有确切的数字，但我怀疑订单簿在卖价处几乎深度达到了百万级，因此我们预计会有一些滑点效应。 presumably，这将会非常显著，并且会显著改变我们对 RSI2 策略回报的预期。

现在我知道，很少有对冲基金会仅在 SPY 上交易 RSI2，这只是为了支持理解的一个概念性例子，我想指出我并不是说 RSI2 不具备可扩展性（也不是说它不具备）。要评估可扩展性，我们需要健壮的回测，清楚地估计订单簿、延迟（如果是日内的话）以及其他相关因素对回报的影响。另一个需要考虑的角度是跨资产的可扩展性，以我们的 RSI2 为例，如果我们将 50%分配给 SPY 和 QQQQ，从理论上讲，我们可以减少给定符号上的滑点和其他交易成本的加权影响（即当我们跨资产分散时，每个符号的边际交易成本在降低）。然而，正如 Joshua 在下面的评论部分很好地解释的那样，这种效果并不一定是线性的。

关于可扩展性的其他途径留给感兴趣的读者，他们总是可以通过电子邮件联系我，因为我最近更关注这个问题。此外，对于与我有着相似职业愿望的读者，要记住模型的可扩展性与就业能力直接相关！

量化基金（QF）
