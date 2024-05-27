<!--yml

类别：未分类

日期：2024-05-12 18:57:14

-->

# 量化交易：使用 Estimize 和 I/B/E/S 收益估计数据进行交易

> 来源：[`epchan.blogspot.com/2015/01/trading-with-estimize-and-ibes-earnings.html#0001-01-01`](http://epchan.blogspot.com/2015/01/trading-with-estimize-and-ibes-earnings.html#0001-01-01)

作者：杨高[Estimize](http://www.estimize.com/)

是一个利用“群体智慧”提供市场情报的在线社区。它包含超过 4,500 名买方、卖方和个体分析师的广泛群体来源估计。

[研究](http://www.estimize.com/api)

（来自德意志银行和莱斯大学等）的数据显示，Estimize 的估计比传统卖方分析师的估计更准确。

我们测试的第一个策略是一种

[均值回归策略](http://www.deltixlab.com/research)

由 Deltix 的定量研究团队使用 Estimize 的数据开发。该策略基于这样一个想法：收益公告后的价格通常会从公告前最近 Estimize 估计所驱动的短期趋势中回归。我们在 2012 年 1 月 1 日至 2013 年 12 月 31 日之间对 S&P100 进行了回测。（尽管 Estimize 有 2014 年的数据，但我们没有相应地包含收盘买入和卖出价格的 Center for Research in Securities Prices 的无生存偏差价格数据。）在 5 个基点的单向交易成本下，我们发现回测显示夏普比率为 0.8，平均年收益率为 6%。以下图表是基于每只股票头寸 1 美元的策略累计盈亏。

| ![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiXC7CpKDYxSfowewc-fjhpePsQJpmFhDeiNkQ2zlIXfSUgO5jd7pKnS4lgGxG7JX6ZPdeb7-eUkwKHJ8Vyuua-OYuRWcjfZIUIC_EcoLB1xiJixhwEu-cicHrIsqtMxFTzetlwyg/s1600/Estimize1.png) |
| --- |
| Deltix 均值回归策略与 Estimize 的累计盈亏 |

令我们惊讶的是，与 Estimize 数据相结合的是一种均值回归策略，而不是动量策略，因为收益估计和公告通常会产生价格动量。为了表明这种回报确实是由 Estimize 中的信息驱动的，而不是仅仅由于价格反转，我们提供了一个仅使用价格生成信号的基准均值回归策略：

1. 找到长期 T 和短期 T_s，其中 T 是所有季度估计报告的平均周期，T_s 是最新 20%的所有估计报告的平均周期。

2. 计算股票回报 R over T 和 Rs over T_s，并令 delta = R - Rs

3. 在收益公告前收盘时买入 delta > 0 的股票，并在公告后第二天开盘时退出头寸。

4. 在收益公告前收盘时卖出 delta < 0 的股票，并在公告后第二天开盘时退出头寸。

5. 在整个持仓期间，用 SPY 对冲净敞口。

这个基准显示没有显著的正回报，因此看来 Deltix 的均值回归策略从 Estimize 数据中确实捕捉到了有用的信息。

接下来，我们将比较从华尔街卖方分析师那里收集的 I/B/E/S 传统盈利预测与众包的 Estimize 预测。回测显示了上面描述的相同 Deltix 均值回归策略，但使用 I/B/E/S 预测在同一 S&P100 宇宙和 2012-2013 期间给出了负回报，这再次支持了 Estimize 预测可能更优越的论点。

由于 Deltix 的均值回归策略在使用 I/B/E/S 数据时给出负回报，自然要考虑是否动量策略能取而代之：如果短期平均预估高于长期平均预估（即类似于上面 delta < 0 的情况），我们预计股价将会上涨，反之亦然。

在相同的宇宙和时间段内，这个动量策略的回测结果非常有希望：交易成本为 5 个基点，夏普比率=1.5，平均年回报率=11%。下面的图表是基于每股 1 美元持仓的策略每日盈亏。

| ![Estimize2.png](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgFSCol46wXxxRFvYNd6c5PYGHJ5HoisL34yW_1OK7EzzHHr-OO1Y-IiVE_J56DZbJK6S4suSY3Fr6neslgE8YgnQND6G19EYbV2IAsofnjQLlUrdfdIIpGGAh3A77NMX0PhnZybg/s1600/Estimize2.png) |
| --- |
| 使用 I/B/E/S 的动量策略累计盈亏 |

我们在 2012-2013 年期间尝试了同样的动量策略，但这次使用的是 Estimize 数据，结果产生了负回报。这并不令人惊讶，因为我们之前发现使用 Estimize 数据的均值回归策略产生了正回报。

我们接着在 2010-2012 年期间使用样本外的 I/B/E/S 数据对 S&P100 进行动量策略回测，不幸的是，该策略在那里的表现也不佳。下面是 2010-2014 年间策略的每日盈亏。

| ![Estimize3.png](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEidNjbkwFj65IfsehpkmF6r4DXC9Ibr_QljgxDKCj1QnoTN77FtiC4dUMDLWRM_QVML_8QHmk3HhCttxYAl4souHsVSPYj_620uvGI5-sqJK2dGuXqXg7dMWc-6umRFpel4DBCOpg/s1600/Estimize3.png) |
| --- |
| 使用 I/B/E/S 的动量策略累计盈亏 |

那么 Deltix 的带有 Estimize 数据的均值回归策略在这个样本外的期间会怎样表现呢？不幸的是，我们不知道，因为 Estimize 直到 2011 年底才开始收集数据。下面是使用不同数据集和期间的不同策略的年回报总结表。

因此，我们无法得出结论，Estimize 数据在产生 alpha 方面始终比 I/B/E/S 数据更好：这取决于所采用的策略。我们也不能决定哪种策略——均值回归或动量——始终更好：这取决于时间段和所使用的数据。我们唯一可以得出结论的是，Estimize 数据的短期持仓加上我们 2014 年缺乏适当的价格数据，这意味着我们无法进行具有统计学意义的回测。这种不明确的状况当然会随着时间的推移而得到解决。

_________

===

**行业动态**

（我们提及的公司或产品并不代表对其进行背书。）

+   有一篇很好的讨论，比较了[Quantconnect](http://quantconnect.com/)和 Quantopian [在此](http://www.quora.com/Quantitative-Finance/What-are-the-advantages-and-disadvantages-of-Quantopian-v-Quantconnect)。

+   对于外汇交易员来说，[Rizm](http://rizm.io/)提供了与 Quantconnect 和 Quantopian 相当的服務，因为它直接连接到 FXCM。

+   Quantopian 现在提供免费的晨星基本数据。同时，查看他们的[Quantopian 经理计划](https://www.quantopian.com/posts/announcing-the-quantopian-managers-program)，在那里你可以竞争管理真实资金。

===

**研讨会更新**

我们下一次的在线研讨会将是

[毫秒频率交易](http://www.epchan.com/workshops/)

日期为 3 月 25 日至 26 日。这是针对那些对日内交易感兴趣的交易员（即使不是以毫秒频率）以及那些想要防御

*对抗*

某些高频交易策略。

===

**管理账户计划更新**

===

关注我 Twitter: @chanep
