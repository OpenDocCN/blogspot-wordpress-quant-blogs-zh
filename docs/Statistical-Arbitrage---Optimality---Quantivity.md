<!--yml

类别：未分类

日期：2024-05-18 13:54:49

-->

# Statistical Arbitrage & Optimality | Quantivity

> 来源：[`quantivity.wordpress.com/2009/12/28/statistical-arbitrage-optimality/#0001-01-01`](https://quantivity.wordpress.com/2009/12/28/statistical-arbitrage-optimality/#0001-01-01)

对统计套利（statarb）策略感兴趣的读者可能会喜欢对两篇最近文章的简要回顾：[美国股市市场的统计套利](http://www.math.nyu.edu/faculty/avellane/AvellanedaLeeStatArb071108.pdf)由 Avellaneda 和 Lee（2009 年 6 月 15 日草稿）以及[最优统计套利交易的分析解决方案](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1505073)由 Bertram（2009 年 11 月 12 日草稿）撰写。

Avellaneda 和 Lee 回顾了 1997 年至 2007 年期间统计套利的结果，重点关注了两种经典方法：协整（beta-neutralized sector ETFs）和[PCA](http://en.wikipedia.org/wiki/Principal_component_analysis)（因子和市场中性化的特征组合）。这是关于统计套利方法的一篇非常简洁的总结，除了几篇早期发表的博士论文之外(*例如* Burgess)。第六部分很有趣，因为它提出了成交量加权回报（最初由技术分析普及）与“交易时间”内测量回报（最近由 Dacorogna 等人普及）之间的等价性；使用这种调整可以增加 37%的 Sharpe 比率（从 1.1 增加到 1.51，承认这并不算太出色）。鉴于成交量加权和“交易时间”在各种定量策略中的广泛适用性，这篇文章值得一读。

伯特拉姆提出了“带有交易成本的最优统计套利策略”的闭形式解，来源于实值积分的泰勒级数逼近。一个有趣的成果，来自第 3.1 节，是断言*最优进入和退出带是关于零对称的*（这与历史实践不同，后者这些预期都是*ad hoc*并且倾向于不对称）。其他有趣的成果是交易长度和策略回报的均值和方差的闭形式解。

伯特拉姆的文章遵循技术风格，重点强调随机过程，源于他的 2005 篇论文：[通过澳大利亚证券交易所数据的实证调查建模资产动态](http://ses.library.usyd.edu.au/handle/2123/1593)。这两篇文章都值得一读，尽管它们都有些正式。
