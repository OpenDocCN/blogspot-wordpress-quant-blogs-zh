<!--yml
category: 未分类
date: 2024-05-18 14:00:39
-->

# Model Scalability – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2011/02/15/models-scalability/#0001-01-01](https://quantumfinancier.wordpress.com/2011/02/15/models-scalability/#0001-01-01)

When designing a model, an aspect that I often overlook is scalability. First a definition from Investopedia: “A characteristic of a system, model or function that describes its capability to cope and perform under an increased or expanding workload. A system that scales well will be able to maintain or even increase its level of performance or efficiency when tested by larger operational demands.”

Now most of you probably wonder why I would overlook such a crucial aspect of model building. The reason is very simple; I never had to. Most of the models I design are for my personal trading and since I don’t have millions of dollar in capital to trade (yet!), the scalability requirements are very insignificant. Most of my trading is on the mini futures and I only trade a few contracts per symbol. Keeping this in mind, I don’t have to worry too much about slippage when I place my orders since the effect of the order book are negligible. However, chances are I am not going to design models solely for my personal trading during my career.

The scalability requirement for a hedge fund for example is however, very different. Imagine trading a high-turnover strategy on a single symbol, for the sake of example, consider a RSI2 strategy. It is a very short term strategy that has a relatively high turnover for an end-of-day strategy. Now trading this strategy with 50k is feasible (not optimal but not too bad), now think about trading the RSI2 signal on a single symbol with 100mm; very impractical. Think how much slippage would affect the strategy. At time of writing, the SPY opened at 133.02, trading 100mm would end up being about 751,654 shares at open quote. Admittedly, I don’t have the exact number, but I doubt that the order book opened almost a million deep at the ask and therefore we would expect some slippage effect. Presumably, it would be quite significant and would significantly change our expectation of return for our RSI2 strategy.

Now I know that few hedge funds would trade a RSI2 on the SPY alone, it is only a conceptual example to support understanding, and I want to point out that I am not saying that RSI2 is non-scalable (nor that it isn’t). To evaluate scalability, we need robust backtesting clearly estimating the impact of the order book, latency (if intraday), and other relevant factors on the returns. Another angle to consider is scalability across assets, following our RSI2 example, if we allocate 50% to both the SPY and the QQQQ, in theory we reduce the weighted impact of slippage and other transaction costs on a given symbol (ie. the marginal transaction cost per symbol is decreasing when we diversify across assets). However, that effect is not necessary a linear one as nicely explained by Joshua in the comment section below.

Other avenues to consider in scalability are left to the interested reader who can always contact me via email if they desire since I have recently paid closer attention to the issue myself. Furthermore, for readers with similar career desires to mine, remember that models scalability is directly related to employability!

QF