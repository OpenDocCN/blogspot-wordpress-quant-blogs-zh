<!--yml

category: 未分类

date: 2024-05-12 18:59:15

-->

# 量化交易：与价格相比，对数价格的共整合交易

> 来源：[`epchan.blogspot.com/2013/11/cointegration-trading-with-log-prices.html#0001-01-01`](http://epchan.blogspot.com/2013/11/cointegration-trading-with-log-prices.html#0001-01-01)

在我最近的

[book](http://www.amazon.com/dp/1118460146/ref=as_li_qf_sp_asin_til?tag=quantitativet-20&camp=14573&creative=327641&linkCode=as1&creativeASIN=1118460146&adid=00W7DZWKQ8DNBM541YD6&&ref-refURL=http%3A%2F%2Fepchan.blogspot.ca%2F)

，我突出了价格差距和对数价格差距的共整合（配对）交易之间的差异。假设两只股票 A 和 B 的价格差距 hA*yA-hB*yB 是平稳的。我们应该保持股票 A 和 B 的

**股票数量**

在比例 hA:hB 固定，当这个差距远高于平均水平时，我们做空这个差距，当这个差距远低于平均水平时，我们做多这个差距。另一方面，对于一个对数价格差距 hA*log(yA)-hB*log(yB)是平稳的情况，我们需要保持股票 A 和 B 的

**市场价值**

股票 A 和 B 的比例（hA:hB）固定，这意味着在每个交易日结束时，由于价格变动，我们需要重新平衡 A 和 B 的股份。

对于我研究过的大多数共整合对，价格差距和对数价格差距都是平稳的，所以我们使用哪种对于我们的交易策略并不重要。然而，对于一个不寻常的对，其中对数价格差距共整合但价格差距不共整合（感谢 Adam G.指出了这样一个例子），其影响非常显著。一个平稳的价格差距意味着价格差异是均值回归的，一个平稳的对数价格差距意味着收益差异是均值回归的。例如，如果股票 A 的增长速度通常比 B 快 2 倍，但最近增长速度比 B 快 2.5 倍，我们可以预期未来增长速度差距会减小。我们仍然做空 A 并做多 B，但当 A 与 B 的增长速度恢复到 2:1 的比例时，我们退出这个头寸，而不是当 A 与 B 的价格差距恢复到历史平均水平时。事实上，A 与 B 的价格差距应该在长期内继续增加。

这部分很容易理解。但多亏了读者 Ferenc F.向我推荐了一篇论文

[Fernholz and Maguire](http://www.jstor.org/stable/4480875)

, 我意识到股票 A 和 B 的对数价格之间存在着简单的数学关系，以便它们共整合。

让我们从这些作者为一个由 2 只股票组成的投资组合的对数市值 P 的变化导出的公式开始：d(logP) = hA*d(log(yA))+hB*d(log(yB))+γ*dt。

此方程中的γ是

γ=1/2*(hA*varA + hB*varB)，其中 varA 是股票 A 的方差

减去

组合市值的方差，varB 同理。

请注意，这个公式适用于任何两只股票的组合，而不仅仅是它们协整的情况。但是，如果它们实际上是在协整，并且如果 hA 和 hB 是创建平稳组合 P 的权重，我们知道 d(logP)不能有一个非零的长期漂移项，该项由 gamma*dt 表示。所以 gamma 必须为零。现在为了使 gamma 为零，

**协方差**

两只股票的协方差必须为正（这里没有惊喜）且等于

**方差的平均值**

两只股票的组合。我邀请读者通过用个别股票的方差和它们的协方差来表示组合市值的方差，来验证这个结论，并将它扩展到包含 N 只股票的组合。这种对数价格的协整检验肯定比常用的 CADF 或 Johansen 检验简单！(为了这种简单性需要付出的代价？我们必须假定收益服从正态分布。)

我的线上量化动量策略研讨会将于 12 月 2 日至 4 日举行。请访问[epchan.com/](http://epchan.com/my-workshops)[我的研讨会](http://epchan.com/my-workshops)页面获取注册详情。
