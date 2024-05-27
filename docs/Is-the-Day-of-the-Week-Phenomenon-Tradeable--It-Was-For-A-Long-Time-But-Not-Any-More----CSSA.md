<!--yml

分类：未分类

日期：2024-05-12 18:47:03

-->

# 星期几现象可交易吗？曾经可以交易很长时间，但现在不行了！| CSSA

> 来源：[`cssanalytics.wordpress.com/2009/09/29/is-the-day-of-the-week-phenomenon-tradeable-it-was-for-a-long-time-but-not-any-more/#0001-01-01`](https://cssanalytics.wordpress.com/2009/09/29/is-the-day-of-the-week-phenomenon-tradeable-it-was-for-a-long-time-but-not-any-more/#0001-01-01)

-   于是我继续了我们这个小时间机器实验，我将星期几的数据输入到学习算法中，以查看是否应该进行交易。结果呢？我得到了一个亮红灯的信号——这意味着星期几效应完全无法交易（即便做空这个策略也不划算）。我回溯了不同的“信号”，并发现 1998 年是最后一年被认为是值得交易的。没有深入探讨方法论，自适应时间机器采用“去趋势”数据——这意味着它关注的是（每日）回报（或正在研究的任何时间间隔）减去平均年回报，这样它就不会将趋势效应误认为是我们要测试的具体策略。此外，一个独立的学习算法检测策略本身收益曲线的变化——类似于人类会做的事情：1) 观察表现是否在加速或减速 2) 观察表现是否变得不稳定。当然，这个过滤器充分利用了统计学，但概念是相同的。

正如下面数据所示，周策略实际上在最后的 3000 个交易 bar 之前是可交易的。然而，当我们查看各种置信度筛选器时，在最后的 3000 个交易 bar 中，置信度和平均每日收益之间似乎几乎没有关系。如果有什么的话，当置信度高认为某一天会走高时，表现实际上一直是负面的——部分原因可能与本世纪出现的均值回归效应和新的均值回归“周末效应”有关。要了解更多信息，请查看[这篇文章](http://marketsci.wordpress.com/2008/10/07/weekend-vs-weekday-follow-through-does-friday%e2%80%99s-sentiment-carry-over-to-monday/)。尽管很明显，任何一天周排名本身包含的前一交易日收益信息与其他交易日无关。然而，如果这是主要原因，我们可能会看到更清晰的逆转或更大的线性效应向下。显然，近年来每日收益中引入了大量噪音，我认为这部分是由于市场效率的逐渐提高。第二组图表展示了如何使用排名方法来识别周效应并创建交易策略。这些例子中还使用了去趋势数据。使用称为 DVR（夏普比率 x 权益曲线 R-squared）的统计方法对每天进行排名，在 1997 年之前，样本外的排名与平均每日收益之间有一个明显但不是完美的关系。现在可以更清楚地看到，在最后 3000 个交易 bar 中，无论是绝对收益还是风险调整后的收益，周效应的随机性。更清晰的是，比较 1997 年之前和之后两个多/空周 portfolios 的权益曲线。所以，至少回答一个问题：周现象是否可交易——不再！所以，教训是——始终保持开放心态，但也要确保深入分析策略，并且随着时间的推移，适应并重新审视你的分析是至关重要的。

![DoWconfperf](https://cssanalytics.files.wordpress.com/2009/09/dowconfperf3.jpg)

123

![DoWrankperf](https://cssanalytics.files.wordpress.com/2009/09/dowrankperf1.jpg)

123

![130-30DoW60-97](https://cssanalytics.files.wordpress.com/2009/09/130-30dow60-971.jpg)![130-30DoW3000](https://cssanalytics.files.wordpress.com/2009/09/130-30dow30001.jpg)
