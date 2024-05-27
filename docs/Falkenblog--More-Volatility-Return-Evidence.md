<!--yml

category: 未分类

日期：2024 年 05 月 12 日 20:28:45

-->

# Falkenblog: 更多波动率-回报证据

> 来源：[`falkenblog.blogspot.com/2012/05/more-volatility-return-evidence.html#0001-01-01`](http://falkenblog.blogspot.com/2012/05/more-volatility-return-evidence.html#0001-01-01)

[Robeco 的 David Blitz](http://www.robeco.com/com/eng/institutional_investors/investments_strategies/active_quant/low_volatility_investing.jsp)

通过瞧一个与 Fama-French 3 因子模型的替代来解决低波动异常，它基本上假设股票经理都在关注基准（参见

[基于代理的资产定价和贝塔异常](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=2068535#captchaSection)

）。 如果属实，那么风险的相关度指标不是总回报波动性，而是基准波动性，其中基准是市场。 他称之为“基于代理”的模型，因为标准

[委托-代理问题](http://en.wikipedia.org/wiki/Principal%E2%80%93agent_problem)

在这里，投资者（委托人）将资金交给组合经理（代理人），后者基于他对基准的异于正常的关注进行投资。有大量轶事和数据表明，机构组合经理是基于他们的基准波动性进行评估的，而与投资者的真实想法无关，因此这不是一个非常激进的假设。

使用 CRSP 数据和传统用于测试理论修改的标准 25 大小-账簿/市场 Fama-French 组合，作者使用月度数据产生这些组合的平均“阿尔法”，这些理论上应该为零的截距（因为其他一切都在模型内）。使用 t 统计和联合 F 检验，可以评估哪种方法更适合数据，而基于代理人的模型效果更好（一如往常，还有其他几种测试）。

这不应该是一个大震惊，因为 F-F 3 因子模型假设贝塔“有效”，而我们知道它不是。 根据

[1993 年的 Fama-French](http://www.sciencedirect.com/science/article/pii/0304405X93900235)

这解释了为什么股票的回报率比债券高，更重要的是，如果我们承认贝塔是一个骗局，那么现代金融的大部分构架都需要进行重大改革，而不是微小的调整。

Blitz 的论文揭示了另一个角度。

[Clarke, de Silva 和 Thorley（2010）](http://www.iijournals.com/doi/abs/10.3905/jpm.2010.36.2.052)

引入了一个波动性因子（VMS—Volatile Minus Stable），就像动量因子一样，只是一个反映“波动因子”风险溢价的多头空头组合，尽管这里的风险溢价是负数，所以这就像一个保险费。将这个 VMS 因子添加到 Fama-French 3 因子模型中不如 Blitz 的基于代理的模型好。如果我们能够摆脱将异常添加到我们的“风险因子”中来解释它们，这将是件好事，这项研究支持了这一努力。

我一直的问题是：如果标准模型是正确的，那么贝塔解释为什么股票比债券风险更高，却不能解释股票内部的回报，这意味着持有高于平均贝塔的股票的人们要么被蒙骗，要么不在均衡状态下。解决方案似乎像是对重大问题的一个要点修补，但却不会引起不一致性上的不安。常识是懂得哪些不一致性是致命的，哪些是噪音，而我的蜘蛛感一直告诉我这是一个严重的不一致性。

与此同时，在这个问题上有很多研究

[让我犯迷糊的](http://www.youtube.com/watch?v=XF2ayWcJfxo)

，因为他们的数据与我看到的数据有很大不同。例如，一些

[法国高等商学院（EDHEC Business school）的研究人员](http://www.edhec-risk.com/edito/RISKArticleEdito.2011-09-20.1606)

一份研究表明，如果你看一个月的持有期，回报会下降，但如果你在 24 个月的持有期内观察，回报会相当持续地上升。 我不明白他们是怎么做到的，但怀疑这与他们的纳入要求有关，例如只包括在随后 24 个月内存在的股票。 此外，他们没有规模排除，因此他们可能使用了每一笔小资产股票，这些股票产生了超额回报，但从实际上来看是不可交易的。 我只是在猜测，因为我不明白他们是如何得到这样一个大的波动溢价（它们使用了几种相同的效果）。

来自 *股票间存在风险/回报权衡吗？*

表 1：多组合分析的几何平均回报。1963 年 7 月至 2009 年 12 月。

另一方面，最近自称为低波动率投资之父的 Bob Haugen 及其忠实合著者 Nardin Baker 纷纷放大了对该异常标准估计的影响。 在

[世界范围内所有可观察市场中低风险股票表现优越](http://www.lowvolatilitystocks.com/bob-haugen-index2/low-risk-stocks-article/)

，通过一个可下载的电子表格，他们发现庞大的

**19％的年化回报差异**

1990-2011 年间在美国最低和最高波动率十分位之间。

我认为 Haugen 和 Baker 看到了问题所在，而与 EDHEC 小组相反。 然而，我也认为他们对此进行了五倍的加强。。
