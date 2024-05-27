<!--yml

分类：未分类

日期：2024-05-12 19:02:14

-->

# 量化交易：风险指标

> 来源：[`epchan.blogspot.com/2011/12/risk-indicators.html#0001-01-01`](http://epchan.blogspot.com/2011/12/risk-indicators.html#0001-01-01)

在 2008 年的金融危机期间，我

[写过相关内容](http://epchan.blogspot.com/2008/10/how-does-financial-crisis-affect.html)

如何观察一些风险指标，比如

[VIX](http://finance.yahoo.com/q?s=%5EVIX)

或者

我需要用[TED spread](http://www.bloomberg.com/apps/quote?ticker=.TEDSP:IND)来决定我的交易策略中应该使用多少杠杆。结果证明，这一过程对于始于 2011 年 8 月的当前危机同样至关重要。实际上，它们不仅仅是用来确定杠杆的因素，还可以作为决定某种策略是否应该实施的重要变量。（如果你认为低杠杆的模型会亏钱，运行这个模型有什么意义？）现在有这些风险指标中可供选择的已经不止几个了。除了 VIX 和 TED，还有[VSTOXX](http://www.stoxx.com/indices/index_information.html?symbol=V2TX)（EURO STOXX 50 波动率）、[VXY](http://www.bloomberg.com/apps/quote?ticker=JPMVXYG7:IND)（摩根大通 G7 波动率指数）、[EM-VXY](http://www.bloomberg.com/apps/quote?ticker=JPMVXYEM:IND)（摩根大通新兴市场波动率指数）、ETF 的[ONN](http://finance.yahoo.com/q?s=ONN)和[OFF](http://finance.yahoo.com/q?s=OFF&ql=1)，以及我可能还没有听说过的许多其他指标。关于我们是否可以根据一些复杂的模式识别算法设计“政权切换”（[regime switching](http://epchan.blogspot.com/2008/05/machine-learning-regime-switching.html)）模型，来决定市场是否处于某种有利于这个或那个特定模型或参数集的“政权”，已经进行了大量学术研究。通常，这些政权切换模型依赖于对历史价格序列中一些复杂模式的识别。很遗憾，我没有发现这些复杂的政权切换模型有任何真正的样本外预测能力。另一方面，我的研究显示，前面提到的某些简单风险指标确实可以防止一些交易模型跌落悬崖。但这些指标中哪些适用于哪个模型？这并不是那么明显。例如，你可能会认为 EM-VXY 对于涉及新兴市场货币的外汇交易模型是一个理想的前瞻性指标，但我发现它只是与我的一致（因此无用）的指标。另一个例子，我在 2008 年金融危机期间说 VIX 似乎对于股票交易模型是一个无用的前瞻性指标，但奇怪的是，它对 FX 模型是一个好的前瞻性指标。相比之下，2008 年每个人都对 TED spread 着迷，当时它飙升超过 300 个基点，但这次从未超过 100 个基点。所以，真正严格的回测才能指导我们。你们用什么风险指标？你们真的回测过它们的有效性吗？在这里您的评论将非常受欢迎。
