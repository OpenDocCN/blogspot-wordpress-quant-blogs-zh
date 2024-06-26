<!--yml

分类：未分类

日期：2024-05-12 18:56:03

-->

# 量化交易：构建内部交易数据库并预测未来股票回报

> 来源：[`epchan.blogspot.com/2017/07/building-insider-trading-database-and.html#0001-01-01`](http://epchan.blogspot.com/2017/07/building-insider-trading-database-and.html#0001-01-01)

===

我长期以来一直对公司内部人士的行为以及他们的行为可能如何影响公司股价感兴趣。我过去在这方面做了一些研究，尽管使用的是非常低科技的方法，主要是 Excel。这是一个高度引人入胜的主题，直观上与公司的股权表现相一致——如果那些最知情的人在购买，似乎股票表现良好是有道理的。如果内部人士在出售，则暗示相反。现实证明比这更复杂，但已经有大量文献对这个[主题](https://scholar.google.com/scholar?hl=en&q=insider+trading&btnG=&as_sdt=1%2C22&as_sdtp=)进行了研究，并在[先前的研究](https://www.amazon.com/Investment-Intelligence-Insider-Trading-Press/dp/0262692341/ref=sr_1_1?ie=UTF8&qid=1500148884&sr=8-1&keywords=nejat+seyhun)中显示是具有预测性的。为了完成西北大学的预测分析硕士项目，我想到运用一些更为突出的机器学习算法来研究内部人交易可能会是一个有趣的练习。然而，我担心随着时间的推移，市场变得更加聪明，内部交易信号的回报可能也已经衰减，正如随着时间的推移被广大观众知晓的策略一样。现在比过去任何时候信息都更容易获得。不久前，投资者需要访问证券交易委员会（SEC）的办公室以获取内部文件。标准提交文件，即表格 4，自 2003 年起只要求电子提交。现在任何人都可以通过[SEC 的 EDGAR 网站](https://www.sec.gov/edgar/searchedgar/companysearch.html)免费获得。如果所有这些数据都只是放在那里，它还能继续提供价值吗？我决定通过直接从 EDGAR 网站抓取文件来查询。尽管有许多数据提供者可供选择（需要支付费用），但我想要直接解析原始数据，因为这将允许与底层数据有更大的“亲密”接触。我在职业生涯的大部分时间里担任数据库开发人员/管理员，所以处理原始文本/xml 并将它们转化为数据库结构似乎很有趣。此外，因为我希望这成为一个真正的端到端数据科学项目，包括通常看起来不那么美观的[80%的实际努力](http://blog.revolutionanalytics.com/2014/08/data-cleaning-is-a-critical-part-of-the-data-science-process.html)——数据整理，这是一个重要的要求。说到这一点，挖掘和整理数据是一项庞大的工作。我花了几个周末来编写代码，最终下载了 240 万个独特的文件。我严重依赖 PowerShell 脚本来首先解析文件并将 XML shredded 到 MS SQL Server 的数据库表中。利用 2005 年至 2015 年的数据，最初的 240 万个记录被过滤 down to 650,000 个内部人股权购买交易。我之所以关注购买而非出售，是因为出售的信号可能会有些模糊。内部人出售有无数个无辜的理由，包括分散投资和支付生活费用。此外，我之所以关注股权交易而非衍生品交易，也是因为类似的原因 - 解读各种衍生品交易背后的动机可能很困难。然而，公开市场的购买订单通常是非常清晰的。经过一些仔细的清理后，我拥有了 11 年的有用 SEC 数据，但除此之外，我还需要定价和市值数据，最好是考虑到生存偏差/已破产公司的数据。Zacks 股权价格和 Sharadar 的核心美国基本面数据集解决了这个问题，而且我可以通过[Quandl](https://www.quandl.com/)以合理的价格（大约每个季度$350）获得这两个数据集。为了探索性数据分析模型建立，我使用了 R 编程语言。我所使用的模型包括线性回归、递归分割、随机森林和乘性适应性回归样条（MARS）。我本打算使用支持向量机（SVM）模型，但在我的笔记本上运行时遇到了性能问题，因为我的笔记本只有 4 个核心。SVM 在缩放方面有困难。不幸的是，我在经历了 10-12 次崩溃后，未能克服这个问题，不得不放弃努力。对于递归分割和随机森林模型，我使用了来自微软 RevoScaleR 包的函数，该包允许与标准基于树的包（如 rpart 和 randomForest）相比具有令人印象深刻的可扩展性。可以期待类似的结果，但 RevoScaleR 包充分利用了多个核心。我将我的数据分为 2005-2011 年的训练集、2012-2013 年的验证集以及 2014-2015 年的测试集。尽管测试集中每个算法的表现相当相似，但最终随机森林胜

无论如何，这是一个很有趣的练习，我从中学习到了很多关于内部交易及其对未来回报影响的知识。或许我们可以得出这样的结论：随着时间的推移，这一信号已经减弱，因为市场已经吸收了内部交易数据的 informational value。然而，或许未来进一步的研究、额外的特征工程和巧妙地考虑额外的算法是值得追求的。

*约翰·J·雷尔，CFA 与妻子和两个孩子一起居住在波士顿地区。他在一家对冲基金担任软件开发人员，是西北大学预测分析硕士课程（2017 年）的毕业生，是一位巨大的网球爱好者，也是机器学习的热心者。您可以通过 john@jryle.com 联系到他。*

===

**陈博士即将举办的研讨会**

在过去的几年里，均值回归策略已被证明是最稳定的赢家。然而，并不是所有的均值回归策略在所有的市场和所有的时间都有效。本次研讨会将为您提供基本的统计技术，让您独自发现均值回归市场，并描述其中一些交易的详细机制。

===

行业更新

+   【脚本制造商】(https://scriptmaker.net/) 允许用户记录订单簿数据用于回测。

+   【成对交易实验室】(https://www.pairtradinglab.com/) 提供了一个基于网页的平台，便于对成对交易策略进行简单的回测。
