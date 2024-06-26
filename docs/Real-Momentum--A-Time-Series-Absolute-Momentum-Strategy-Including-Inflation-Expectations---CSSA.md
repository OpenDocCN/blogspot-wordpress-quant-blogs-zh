<!--yml

category: 未分类

date: 2024-05-12 17:46:49

-->

# Real Momentum: A Time-Series/Absolute Momentum Strategy Including Inflation Expectations | CSSA

> 来源：[`cssanalytics.wordpress.com/2015/05/07/real-momentum-a-time-seriesabsolute-momentum-strategy-including-inflation-expectations/#0001-01-01`](https://cssanalytics.wordpress.com/2015/05/07/real-momentum-a-time-seriesabsolute-momentum-strategy-including-inflation-expectations/#0001-01-01)

![inflation](https://cssanalytics.files.wordpress.com/2015/05/inflation.png)“[Time-Series Momentum](http://pages.stern.nyu.edu/~lpederse/papers/TimeSeriesMomentum.pdf)”由 AQR 的 Moskowitz 和 Pedersen 在 2011 年左右提出，并由 Antonacci 在 2013 年将其普及为“[Absolute Momentum](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=2244633)”。这两种方法都通过回顾某个时间窗口内的资产回报超过无风险利率的程度，来决定是否持有给定资产的多头仓位，或者持有现金或者做空。这种方法已经被趋势追随者以某种形式使用了几十年。Moskowitz 和 Pedersen 关于这一主题的学术研究证明了这种效应在不同市场的广泛多样性中的稳健性。Antonacci 展示了如何在这种方法中包括战术策略，包括资产类别，以及如何通过“双重动量”与相对强度相结合。

这个概念一直对我很有吸引力，而且使用这种方法来降低持有选定资产类别的下行风险是有道理的。在思考这个概念时，我能理解为什么超额回报（或回报减去无风险利率）在理论上是吸引人的，因为这是现代金融经济学理论的基础。但我也意识到，投资者并没有获得名义回报——他们获得的是经通胀调整后的实际回报。生活成本上升，因此名义回报必须跟上通胀的步伐，才能使投资者的投资获得真正的回报。投资者避免持有负超额回报的资产是理性的.*（注意，原文中最后一句有一个未完成的句子，所以在翻译时我将其补充完整）*

挑战在于，通胀是相当难以捉摸的。像消费者价格指数（CPI）这样的指标每月发布一次，存在滞后，并且最多只能算是一个典型消费者商品成本变化的模糊度量。获取实时通胀估计的一个最佳方式可能是观察国债通胀保护证券（TIPS）与常规国债债券相当期限的收益率曲线。这两者之间的差异代表了前瞻性的预期通胀。由于通常没有与 TIP 相比的传统国债相匹配的债券期限，这个真实收益率需要使用非线性估计进行插值。快速而方便（尽管不完美）地捕捉这个差异的方法是观察 7-10 年国债债券（IEF）与国债通胀保护债券（TIP）之间的回报差异，这两者都是每日交易的 ETF。两者有效期限大约为 8 年，大致等效。它们总回报的日差异本质上代表了预期通胀的变化。由于这可能有些嘈杂，我选择使用 10 日平均来平滑这个数据。为了代理无风险利率，我使用短期国债或（SHY）。为了计算“真实动量”，我使用每日真实超额回报的平均值。这本质上是一个资产的日回报减去无风险利率（SHY）和预期通胀（TIP 和 IEF 之间日回报差异的 10 日移动平均）的平滑回报。

**真实动量**=资产回报-无风险回报-预期通胀

或者简单移动平均的：

资产的日回报-无风险代理（SHY）的日回报-预期通胀代理（TIP-IEF 平滑）的日回报

为了与绝对或传统的时间序列动量进行比较，使用一个平均每日回报代理是重要的，这个代理仅仅是某资产的每日超额回报减去 SHY 的回报的平均值。以下是比较真实动量与绝对动量从 2005 年（6 月）至今使用 S&P500（SPY）的结果。请注意，TIP 的数据有限，所以这是可以适应不同回顾期的最早开始日期的大致估计。

![真实绝对动量](https://cssanalytics.files.wordpress.com/2015/05/real-abs-mom.png)

在这 10 年的时间里，看起来真实动量（Real Momentum）要优于绝对动量（Absolute Momentum），这与我们从理论上可能预期的相符。从视觉检查来看，这种差异似乎微不足道。但我对这些初步测试的结果还不完全确信差异是真实的（无意中双关语）。趋势追踪策略需要大量的数据才能具有统计意义，因为它们交易不频繁。更长的测试周期会更合适，同时测试应包含实际收益率，而不是 TIP/IEF 差异，这不是进行比较的理想基础（这就是为什么平滑处理优于使用原始每日差异的原因）。或者，可以使用一个能回溯更长时间历史的 TIP 替代品。由于这项测试还处于初级阶段，我会提醒说，现在还很难得出任何确切的结论。但真实绝对回报的概念是有吸引力的，只是考虑到通货膨胀本身就可以用多种方式计算，因此在量化方面更加棘手。欢迎分享您关于这个有趣话题的想法/评论和建议。
