<!--yml

分类：未分类

日期：2024-05-18 13:50:20

-->

# 均值回归重申 | Quantivity

> 来源：[`quantivity.wordpress.com/2011/07/03/mean-reversion-redux/#0001-01-01`](https://quantivity.wordpress.com/2011/07/03/mean-reversion-redux/#0001-01-01)

阅读[动量重申](https://quantivity.wordpress.com/2011/06/18/momentum-redux/)的读者要求为均值回归文献写一个类似的帖子，认识到动量和均值回归的阴阳关系。

最有趣的一个转折是交易频率引起的概念性“苹果和橙子”问题；作者使用相同的词语，但意味着不同的事情。这种细微差别、混淆和混淆的机会源于反转*在许多频率上同时显现*：

+   日内：市场制造、交易所套利，以及各种最近的高频交易娱乐

+   日 – 月：因素收敛，无论是协整、主成分分析，还是更现代的维度降维方法（如[流形学习](https://quantivity.wordpress.com/2011/05/08/manifold-learning-differential-geometry-machine-learning/)）

+   月 – 年：“逆向”策略，基于会计、FF 异常或行为模型

由于这种异质性，回归在许多统计形态中显现；或者，用机器学习的语言来说：如果你能提取一个*稳定的时间序列或横截面特征*，你可能可以交易它。

回归最初是针对价格和回报考虑的，无论是单一资产还是篮子。随后，考虑时间序列回归的高阶矩：方差、偏度和峰度。横截面回归也使用各种各样的统计和机器学习广泛研究；最著名的三个：相关性、协整和主成分分析。

相关的交易策略有*许多*名称，取决于频率和市场参与者，包括：统计套利、波动套利、相对价值、长短、收敛、配对、市场制造、*等。每个频率起源的文献，以及继续演变，由于不同的受众而相对独立。

**规模不变性**

这个问题引发了一个有趣的元问题：*为什么回归表现出概念上的规模不变性，而动量则不然*。例如，观察搜索“微观结构动量”和“变异性动量金融”时缺乏意义的结果。

这种区别在概念框架、建模以及相应的数学中普遍存在。一个微观结构解释似乎是合理的：市场制造本质上是有均值回归的，因为它基本上归结为*库存控制*。这与推动动量的行为偏见形成对比，最近的丰富证据通过泡沫频繁的荒谬证实了这一点。

这种解释进一步暗示了可能的计算偏差：市场制造现在是自动化的，而行为偏差是由人类以不同的扩散率吸收信息并遵循非机械规则切换他们的 401K / IRA 分配（或类似地，长期单一基金组合）。这种解释在统计上也很吸引人，因为相当基础的数学可以证明这种组合导致非线性和非平稳信号。

认识到这个区别，以下讨论分为两部分：日内和日间。

**日内回归**

日内均值回归是一种某种形式的市场制造（复杂程度不同），大多数寻求夜间平坦；具有不同的平坦度定义，包括：库存、β暴露、时刻暴露、希腊字母暴露等。回顾过去几十年，专家和“本地人”都实施了非机械回归交易策略。而且，现在人们抱怨前端运行；谈谈印钞机！

[爱德·索普](http://edwardothorp.com)和[理查德·布克斯塔伯](http://rick.bookstaber.com/)都最近回顾了自动化回归技术的起源，他们在 1980 年代初将功劳归于 Gerry Bamberger，同时介绍了[大卫·肖](http://www.deshaw.com/Founder.html)和彼得·穆勒（Process Driven Trading，目前似乎是 PDT Advisors？），他们都是[摩根士丹利](http://www.morganstanley.com/)的前员工。参见[威尔莫特文章](http://edwardothorp.com/id9.html)和[我们自己的设计恶魔](http://en.wikipedia.org/wiki/A_Demon_Of_Our_Own_Design)，分别。

日内回归文献相当贫乏，原因是以下因素（也许还有更多？）：

+   专有：对冲基金经理谨慎地保护这些技术的披露

+   数据可用性：滴答数据难以积累，清理成本高昂，大规模维护复杂；更不用说，交易所几乎没有改变这一点的激励，因为他们的商业模式取决于出售数据

+   成本：日内交易需要低延迟执行，因此不适用于零售

+   计算：日内交易越来越多地涉及计算机工程，因为需要强大的计算基础设施（托管、网络、订单簿等）

由于计算复杂性（执行和大规模数据管理），日内交易越来越多地超越金融和计量经济学，更接近机器学习和计算机科学/工程。虽然这对 Quantivity 来说很有趣，但对于纯金融人士来说，他们处于越来越大的劣势。

在学术上，日内主要是市场微观结构文献考虑的。参见[JFM 编辑委员会](http://www.elsevier.com/wps/find/journaleditorialboard.cws_home/600652/editorialboard)著名研究人员；可以说最著名的三个是[Harris](http://www-bcf.usc.edu/~lharris/), [O’Hara](http://www.johnson.cornell.edu/Faculty-And-Research/Profile.aspx?id=mo19), 和[Hasbrouck](http://pages.stern.nyu.edu/~jhasbrou/)。以下是代表性的微观结构文献：

+   [一项基于交易数据的周内和日内

+   [估计买卖价差组成部分](http://ideas.repec.org/a/eee/jfinec/v21y1988i1p123-142.html)，Glosten 和 Harris（1985）

+   [市场制造的微观经济学](http://www.jstor.org/pss/2330686)，O’Hara 和 Oldfield（1986）

+   [市场制造商的交易：对 NYSE 专家的实证分析](http://www.jstor.org/pss/2329060)，Hasbrouck 和 Sofianos（1993）

+   [专家库存和报价变化分析](http://www.jstor.org/pss/2329061)，Madhavan 和 Smidt（1993）

+   [场内生活：竞争性市场制造和库存控制](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=7464)，Manaster 和 Mann（1996）

+   统计套利统计学，Fernholz 和 Maguire（2007）

+   [短期预期回报中的均值回归](http://www.jstor.org/pss/2962048)，Conrad 和 Kaul（1989）

+   [对冲交易：相对价值套利规则的表现](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=141615)，Gatev, Goetzmann, 和 Rouwenhorst（1998）

如[先前回顾](https://quantivity.wordpress.com/2010/01/12/how-to-learn-algorithmic-trading-part-3/)，关于微观结构的书籍长度处理在[交易与交换：市场微观结构实践者指南](http://books.google.com/books?id=Rd9hDRR1Yx4C)（Harris），[经验市场微观结构](http://books.google.com/books?id=aaReNv846eMC)（Hasbrouck），以及[市场微观结构理论](http://books.google.com/books?id=udXjR2Dg7bwC)（O’Hara）。

**日内反转**

日内反转的起源与[动量](https://quantivity.wordpress.com/2011/06/18/momentum-redux/)相似：技术分析的长久基础，近年来由 EMH 辩论引发的学术处理正式化。尽管这方面的文献同样庞大，以下文章体现了主要的演变点：

+   [股市是否过度反应？](http://www.jstor.org/pss/2327804)，De Bondt 和 Thaler（1985）

+   [股票价格均值回归：证据与含义](http://ideas.repec.org/p/nbr/nberwo/2343.html)，Poterba 和 Summers（1987）

+   [资产价格的共同非平稳组成部分](http://ideas.repec.org/a/eee/dyncon/v12y1988i2-3p347-364.html)，Bossaerts（1988）

+   [当股市过度反应时逆向利润何时产生](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=227214)，Lo 和 MacKinlay（1990）

+   [证券回报的可预测行为证据](http://ideas.repec.org/a/bla/jfinan/v45y1990i3p881-98.html)，Jegadeesh（1990）

+   [时尚、马丁格尔和市场效率](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=227518)，Lehmann（1990）

+   统计套利动态建模的计算方法，Burgess（1999）

+   美国股票市场中的统计套利，Avellaneda 和 Lee（2008）

首先，著名的六大反转和 FF 过激异常，以各种形式出现（毫不奇怪，其中几个名字与[动量](https://quantivity.wordpress.com/2011/06/18/momentum-redux/)文献中有共同之处）。Burgess 论文的巅峰之作，总结了 4 年的自动化研究以及使用初露头角的人工智能技术进行日内反转（参见 Burgess 先前的十多篇出版物）。证明世界很小，Burgess 受雇于……你猜对了，摩根士丹利。最后，Avellaneda 和 Lee 回顾性地调查了这一领域，记录了竞争以及最终的基本日内反转策略的交易平稳。

这一切的奇妙讽刺在于，它确实证实了（不一定无风险）套利的存在：确实可以通过源自这些概念的策略赚钱，除非存在非零时间限制，即可能今天无法实现。证明是通过矛盾：如果这不是真的，相应的对手策略总会成功，从而构成免费的午餐。
