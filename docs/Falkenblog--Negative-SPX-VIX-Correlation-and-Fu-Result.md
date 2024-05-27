<!--yml

分类：未分类

日期：2024 年 05 月 12 日 20:51:19

-->

# Falkenblog：SPX/VIX 负相关和傅的结果

> 来源：[`falkenblog.blogspot.com/2011/06/negative-spxvix-correlation-and-fu.html#0001-01-01`](http://falkenblog.blogspot.com/2011/06/negative-spxvix-correlation-and-fu.html#0001-01-01)

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgtd7ASSiOnufFfDr3kxvhexzX9ZGtntH35utv6wjdqscuWv00A7pItjeIx6BkVAlyu-QHycQDo833nDivDJz6KH44nYN6-YTTI27Cd85XDrOp-HRDc-uZq9mQcBTtnINAfZzCgRg/s1600/spyvix.jpg)

上图是月度百分数变化的图表

[VIX](http://en.wikipedia.org/wiki/VIX)

, 大约等于标准普尔 500 期权波动率和标准普尔 500 本身的回报。存在着明确的负相关模式。这很合理，当市场下跌时波动性增加，反之亦然。如果我告诉你 VIX，或其 ETF

[VXX](http://finance.yahoo.com/q?s=VXX)

, 如果 VXX 上涨很多，那么 SPY 大幅下跌的可能性很大。

但是，如果把日期提前，也就是过去的波动性变化和未来的回报，就没有相关性。波动率水平和股票回报之间存在轻微的负相关。因此，很明显这主要是一个同时的模式应用于波动性变化，而不是一个预测因素。想象一下，在 2008 年，波动率上升时，股价同时下跌。波动率的上升并不能预测价格的变动，仅仅是反映它们，高波动率与 2009 年后期的大幅下跌和大幅反弹都存在相关性。

方建富在 2009 年的 JFE 上有一篇备受引用的论文，

[特异风险和预期股票回报的横截面相关性](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=676828)

，这篇论文声称，与先前报道的特异波动性和未来回报负相关相反，它们实际上是正相关的。他声称，如果你用 EGARCH 模型估计特异波动性，将会扭转之前的研究结果

[Ang et al](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=611363)

, 每个月最高减最低特异波动性十分位数的回报大约为正 1.75%，基本上是平的，除了最高预期波动十分位数存在明显的上升。

我已经查看过这篇论文，相信他犯了一个错误，但我不知道具体是什么。在数据中我看不到这种情况，并且我怀疑他特定的 EGARCH 也不会改变这一点，但很难确切地复现他的方法。他声称‘高特异波动性的股票与高回报同时发生，并且在下个月会逆转。因此，高特异波动性股票的回报在下个月是异常低的’，这个发现我觉得很奇怪，因为这与上文的模式相反，而且不仅适用于指数，也适用于股票。

但是，这对于低波动性交易者来说是个好消息。只要老一辈可以指出他们的结果仍然可行的证据，他们就会相信它，这给那些看透这一点的人留下了更多的机会。用

[西塞罗](http://www.brainyquote.com/quotes/quotes/m/marcustull139337.html)

的话来说，智慧的作用是区分好坏投资。
