<!--yml

category: 未分类

date: 2024-05-12 18:13:26

-->

# Some Subtle Thoughts on Mean-Reversion and How To Create More Informative Benchmarks | CSSA

> 来源：[`cssanalytics.wordpress.com/2011/01/21/some-subtle-thoughts-on-mean-reversion-and-how-to-create-more-informative-benchmarks/#0001-01-01`](https://cssanalytics.wordpress.com/2011/01/21/some-subtle-thoughts-on-mean-reversion-and-how-to-create-more-informative-benchmarks/#0001-01-01)

迈克尔·斯托克斯（Michael Stokes）在 MarketSci 网站上[`marketsci.wordpress.com/`](http://marketsci.wordpress.com/)做了出色的工作，他发布了一份关于“均值回归状态”的非常有趣的研究报告。同样有趣的是，Jez Liberty 在自动化交易系统[`www.automated-trading-system.com/`](http://www.automated-trading-system.com/)所做的关于互补的“趋势跟随状态”的研究。这两份报告都旨在通过类似或相关策略的性能来捕捉某种“效应”。这样的逻辑是，这样的基准应该能在“20,000 英尺的高度”揭示有关给定风格相对有效性的重要信息。我写这篇文章并不是为了贬低/批评这些博主（尤其是迈克尔，因为这里只考虑均值回归）的优秀工作，而是想指出基准本身如何在与任何类型的指数产品相似的方式下创造解释上的问题。其中一些问题是如此微妙——比如“再平衡奖金”，它们值得单独的一篇文章。现在，考虑在博客圈经常提到的“均值回归哲学”上的一些微妙想法是很重要的。在我看来，许多读者可能认为这是理所当然的——或者没有考虑过——但这背后还有许多层次。

最终，我们大多数人认为的“均值回归”实际上是一种语义上的理解，并不一定可以互换。在此阶段，我将避免读者做出具体的定义，而是提到，用一个策略来代表一个群体或构成均值回归效应的基准线实在是过于简单化了。例如，“日常跟进”或其反面似乎是大多数交易员用来代表均值回归的默认标准（需要注意的是，均值回归的状态更加平衡）。在我看来，日常跟进（或者我更愿意称之为反向日常跟进）本身并不是我的理解中的均值回归。这反映了我对观察分类特定特征的条件的思考的最新演变。在这种情况下，日常跟进策略的特点与指示器不同，这些差异并不是一目了然的。因此，观察到的“日常跟进”策略的表现（或最近的缺乏表现）并不能恰当地导致一系列线性结论。混淆并没有就此停止：*均值回归可以在不遵循正负交易日模式的情况下，在每日层面上仍然获利。此外，存在一个获利策略，该策略在消退正/负日期的同时，并不一定意味着强烈的均值回归。这种差异很大程度上与测量给定效应时，十分位数/四分位数/中位数/平均数行为的非线性有关。* 此外，极端值往往出现在高/低波动性或非常强/弱的趋势中，可能会偏见各种回测长度。环境对 1 天滞后性能的微观测有很强的条件效应。此外，当逆势操作时，长期与短期信号的持续错误信号也会模糊实际发生的情况。也就是说，做多/持币与做多/做空非常不同，一方面（即做空）的盈利/亏损可能会掩盖另一方面（即做多）的盈利/亏损。

在指标层面，很难一概而论，因为不同的指标可以衡量不同的事物，有时根据这些差异，它们的性能可能会有很大差异。DV2 或 DVB 指标在 2010 年表现出色，而其他“均值回归”策略则遭受损失——将它的优越性视为一个均值回归指标是愚蠢和自私的，但更重要的是，这也模糊了重点：*DVB 或 DV2 衡量的是相对范围（收盘价与高/低价）的分布，它并不总是一个均值回归指标！* DVB/DV2 倾向于适应当前环境，因为它不在乎相对的收盘价，所以它经常在上涨的日子发出做多信号，在下跌的日子发出做空信号。这 creates a substantial “tracking error” to any benchmark such as daily follow through that looks at the binary pattern of closing prices over the last two days. The RSI2 also need not be a mean-reversion indicator– in this case because it has very different behavior at a binary level (50/50) versus extremes, and also has very different behavior as a function of time spent at extremes. The RSI is more closely related to daily follow through, yet because of these properties as well as a 2-day parameter, it can also generate material tracking error to such a benchmark. The RSI is also a multi-faceted tool that can be used in for example the reverse direction for strongly trending markets. In other words, high readings can function more accurately as a trend signal–especially in commodities. This negates the stereotype that it must function as a pure mean-reversion indicator. The parameter length of the aforementioned examples in itself is ambiguous as it suggests that mean-reversion is defined by a given lookback–in this case shorter-term. Also missing in this discussion is the profitability or derivative of the strategy–that is conditional performance matters.

为了使问题更加复杂，讨论波动率过滤器和相关指标及其与均值回归性能的联系可能会进一步模糊最终目标（这是下一篇文章的主题）。所以让我们退一步，考虑一下我们试图实现什么。均值回归的细微差别确实是无穷无尽的——一个人必须理解指标的计算及其同时假设/缺点，才能理解为什么事情成功或失败。让我们以 RSI2 为例。RSI2 只是一个振荡器，它捕捉的是收盘到收盘点的上升与下降的相对测量。也就是说，它并不考虑开盘价、最低价或最高价。通过重新缩放的过程，这个测量被标准化（尽管更类似于强制非线性压缩）在 0 到 100 之间。RSI 有一些优点和缺点，首先说优点：1)它非常敏感，倾向于与价格同步变动 2)它比使用点移动或回报更正常化，因为它考虑的是相对移动而不是纯粹的绝对移动。这使得创建标准化交易规则变得更容易。现在谈谈缺点：1) RSI 值仍然是相对绝对的，随着时间的推移，值的分布可能会改变，使得极端读数变得更加稀少，反之亦然，尤其是在环境发生变化时（想想 2009 年）。2) 使用 RSI 隐含地假设收盘到收盘的移动是一个平稳且宝贵的未来均值回归预测器——实际上，动量（收盘到收盘）与范围（收盘价与最高价和最低价）的相对重要性可以在短期和长期内发生变化。它们也可能有复杂的相互作用效果。一个例子就是 RSI-DV2 背离，或者指标在孤立使用时背离的性能。继续列举存在的古怪之处或偏差没有多大意义。重点是均值回归是一个高度细微的话题——在没有深入了解细节的情况下，无法有效利用。也许这篇文章有点像那些没有清晰结局的电影——这样的电影需要观众在事后进行一些思考，或者对可能的结局有所想象。如果这篇文章能帮助你在适当的背景下做后者，那么你会发现自己成为一个更好的系统开发者——甚至是一个比使用技术指标更好的主观交易员。
