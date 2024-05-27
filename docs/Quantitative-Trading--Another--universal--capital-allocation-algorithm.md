<!--yml

分类：未分类

日期：2024-05-12 18:57:34

-->

# 量化交易：另一种“通用”资本分配算法

> 来源：[`epchan.blogspot.com/2014/07/another-universal-capital-allocation.html#0001-01-01`](http://epchan.blogspot.com/2014/07/another-universal-capital-allocation.html#0001-01-01)

金融工程师们习惯于从其他领域的科学家那里借鉴技术（例如遗传算法），但很少有反过来借鉴的时候。因此，听说这个

[论文](http://www.pnas.org/content/early/2014/06/11/1406556111.abstract)

关于可能由通用资本分配算法启发的自然选择进化的机制令人惊讶。

资本分配算法试图优化资本在投资组合中分配给股票的方式。被称为

*通用*

如果它导致净资产“相似”于通过时间固定的权重组合生成的最佳常数再平衡投资组合（以下表示为 CBAL*），则视为有效。“相似”在这里意味着净资产不会指数级发散。 （有关精确定义，请参阅非常易读的

[论文](http://arxiv.org/pdf/1107.0036.pdf)

由博罗丁，

*等等*

. 致谢：弗拉基米尔·P.)

以前，我只知道这样一个通用的交易算法——由托马斯·考弗发明的通用投资组合，我已描述

[之前](http://epchan.blogspot.ca/2007/01/universal-portfolios.html)

. 但这里有一个被证明是通用的方法：极其简单的

[EG 算法](http://www.cis.upenn.edu/~mkearns/finread/helmbold98line.pdf)

.

EG 算法（Exponentiated Gradient）是使用“乘法更新”的资本分配规则的一个例子：分配给一只股票的新资本与其当前资本成比例，乘以一个因子。这个因子是该股票上期回报的指数函数。这个算法既贪婪又保守：贪婪是因为它总是将更多资本分配给最近表现最好的股票；保守是因为从一期到下一期改变分配过于剧烈会有惩罚。这种乘法更新规则是自然选择进化模型的提议。

EG 算法相对于通用投资组合的计算优势是显而易见的：后者需要在每个步骤中对所有可能的分配进行加权平均，而前者只需要知道最近一段时间的分配和回报。但这个 EG 算法实际上在实践中能产生良好的回报吗？我用了两种方法来测试它：

1) 在现金（年利率 2%）和 SPY 之间分配。

2) 在标普 500 股票之间分配。

在这两种情况下，模型唯一的自由参数是一个称为“学习率” η 的数字，它决定了分配如何从一个时期变化到下一个时期。通常发现 η=0.01 是最佳的，我们采用了这个值。此外，在这个研究中，我们不允许空头头寸。

对于 1) 的比较基准是，使用 Borodin 论文的符号

a)  持有并 SPY 组合

**BAH**

，和

b) 最佳常重平衡组合，回顾时固定的分配

**CBAL***

。

比较基准 2)的是

a) SP500 股票的常重平衡组合，分配相等

**U-CBAL**

，

b) 回顾时选择最好的股票，分配为 100%

**BEST1**

，和

c)

**CBAL***

。

为了找到 SP500 组合的 CBAL*，我使用了 Matlab 优化工具箱的有约束优化函数

*fmincon*

。

还有一个 SP500 指数重建的问题。在有约束的优化函数中处理指数的增加和删除是很复杂的。所以我选择了使用 2007 年至 2013 年间 SP500 中的股票子集的快捷方式，容忍生存偏差的存在。这样的股票只有 346 只。

对于 1) (现金对 SPY)的结果是 EG 的复合年化增长率（CAGR）略低于 BAH（4% 对 5%）。结果表明 BAH 和 CBAL* 是一样的：在 2007-2013 年间最好将 100%分配给 SPY，这在事后看来是一个毫不令人惊讶的建议。

对于 2) 结果是 EG 的 CAGR 高于等权重组合（0.5% 对 0.2%）。但这两个数字都远低于 BEST1（39.58%），这与 CBAL*（39.92%）几乎相同。（你能猜出当前 SP500 中哪个股票产生了最高的 CAGR 吗？答案，将在下面揭示*，会让你大吃一惊！）

我们被告知 EG 算法将表现得“类似”于 CBAL*，那么为什么它的表现如此糟糕？记住这里的相似性只是指分歧是亚指数的：但即使是多项式分歧在实践中也可能很大！这似乎是资产配置的通用算法的问题：我从未找到过任何在短短几年的时间里实际上取得显著回报的算法。也许我们会在更高频率的数据中找到更多有趣的结果。

所以鉴于 EG 的令人失望的表现，我为什么还要写关于这个算法，除了它与生物进化的有趣联系之外？那是因为它为另一个，

非

-通用，组合分配方案，以及优化交易策略参数的一般方法：这两个主题留待下次讨论

===

**研讨会更新:**

我的下一个在线研讨会将在

[均值回归策略](http://www.epchan.com/my-workshops/)

8 月 26 日至 28 日。

[这个](http://www.nbs.ntu.edu.sg/Executive_Education/NTU_SGX_Centre_for_Financial_Education/Documents/ATC-%20MEAN%20REVERSION%20STRATEGIES.pdf)

和

[量化动量](http://www.nbs.ntu.edu.sg/Executive_Education/NTU_SGX_Centre_for_Financial_Education/Documents/ATC-%20QUANTITATIVE%20MOMENTUM%20STRATEGIES.pdf)

研讨会也将在新加坡南洋理工大学现场举行，时间是 9 月 18 日至 21 日。

**===**

请关注我

[关注 Chanep](https://twitter.com/intent/follow?original_referer=http%3A%2F%2Fepchan.blogspot.ca%2F&region=follow_link&screen_name=chanep&tw_p=followbutton&variant=2.0)

我在 Twitter 上也会分享有趣的文章链接。

**===**

从 2007 年到 2013 年，SP500 股票中回报最高的是 AMZN.*
