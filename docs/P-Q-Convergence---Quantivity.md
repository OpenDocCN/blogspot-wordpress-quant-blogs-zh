<!--yml

分类：未分类

日期：2024-05-18 13:48:47

-->

# P-Q 收敛 | Quantivity

> 来源：[`quantivity.wordpress.com/2011/09/21/p-q-convergence/#0001-01-01`](https://quantivity.wordpress.com/2011/09/21/p-q-convergence/#0001-01-01)

许多聪明的人在预示量化金融将发生根本性变革。对于数学倾向者来说，这种变革具有巨大的阿尔法潜力，并将导致那些试图[学习算法交易](https://quantivity.wordpress.com/2010/01/10/how-to-learn-algorithmic-trading/)的人面临*更高*的技术门槛。而那些买入并持有的投资者则可怜。

不同的人以不同的俚语方式收敛于这种变革。[Derman](http://blogs.reuters.com/emanuelderman/) 将会出版一本批评金融过度建模的书。 [Taleb](http://www.fooledbyrandomness.com/) 多年来一直在写有关不慎使用数学假设的书。 [Haug](http://www.espenhaug.com/articles.html) 在几篇论文中揭穿了 Black-Scholes 的理论。 [Bouchaud](http://www.cfm.fr/us/organisation.php) 和 [Potters](http://www.cfm.fr/us/organisation.php) 花了十年时间通过质疑经典教条来普及经济物理学。 [Meucci](http://www.symmys.com/attilio-meucci) 写了一本[书](http://books.google.com/books?id=Qc8KWWtUokcC) 并多年来一直在教授这门课。 [Sornette](http://www.er.ethz.ch/people/sornette) 通过研究崩溃建模和预测正在创造量化宏观经济。甚至大银行的人员也加入进来，比如最近由 Petrelli *等人*撰写的论文。

尽管用词不同，但归根结底都是同一个根本性变化：**![\mathbb{P}](img/f2d0e071de256bbddee88d21a6582414.png) 和 ![\mathbb{Q}](img/969ce5c634b2b4963929a6476f8ccc63.png) 世界的收敛**。金融危机刺破了![\mathbb{Q}](img/969ce5c634b2b4963929a6476f8ccc63.png) 风险中性的纯粹数学世界，为与真实世界的![\mathbb{P}](img/f2d0e071de256bbddee88d21a6582414.png) 双向协同关系的种子奠定了基础。

对于不熟悉的人来说，![\mathbb{P}](img/f2d0e071de256bbddee88d21a6582414.png) 和 ![\mathbb{Q}](img/969ce5c634b2b4963929a6476f8ccc63.png) 是两种不同的金融传统的简称（参见[Meucci 2011](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1717163)）。![\mathbb{P}](img/f2d0e071de256bbddee88d21a6582414.png) 是买方的投资组合管理世界，包括零售、专有以及大部分的基金世界（以及很多养老金和保险业）。![\mathbb{Q}](img/969ce5c634b2b4963929a6476f8ccc63.png) 是卖方的衍生品世界，最好的例子是异构（以及在较小程度上的结构化产品）。历史上，这两个世界的差异非常大（*例如* 比较 [mathbabe](http://mathbabe.org/) 与 [Falkenstein](http://falkenblog.blogspot.com/)）。

粗略和不公平地描述他们的历史传统：![\mathbb{Q}](img/969ce5c634b2b4963929a6476f8ccc63.png)是前物理学家从事数学上美丽的偏微分方程和随机微积分（因此与统计力学和相关领域相似），由希望预订利润和转移风险的交易员推动；![\mathbb{P}](img/f2d0e071de256bbddee88d21a6582414.png)是投资组合经理，通过应用主要是马科维茨/布莱克-利特曼传统的基本统计和优化来建立投资模型。值得注意的是，这两个世界都没有来自旧交易所本地人的后代，他们在没有数学的情况下生活：价差、执行效率和技术（包括纯玩 HFT）。

这场变革在于*这两个世界开始日益模糊*，随之而来的是 alpha 的迁移。

第一个模糊现象是统计套利。可以说大型量化基金之所以出名，正是因为他们认识到了![\mathbb{P}](img/f2d0e071de256bbddee88d21a6582414.png)——![\mathbb{Q}](img/969ce5c634b2b4963929a6476f8ccc63.png)的收敛性，并建立了相应的大规模建模和执行专业知识。在过去的几年里，这种收敛性开始加速：花几分钟浏览一下[王 2009](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1428555)和[佩特雷利 2010](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1530046)。量化从来没有读过更公开对抗性的学术文章（由大银行的人写的），也没有更多使用斜体字的。然而，在阅读时，量化点头表示赞同，因为量化已经交易了多年的统计和波动套利。

最重要的是，这种模糊现象正在*零售量化项目*中出现。这不是学术界保留的理论辩论。

取数百万零售投资者面临的两个典型例子：代理对冲和最优衍生品清仓。两者都有各自文献中的“解决方案”——然而在现实生活中它们荒谬地不令人满意。代理对冲来自![\mathbb{P}](img/f2d0e071de256bbddee88d21a6582414.png)，在处理基差风险时几乎完全忽视了![\mathbb{Q}](img/969ce5c634b2b4963929a6476f8ccc63.png)的处理（当然，![\mathbb{Q}](img/969ce5c634b2b4963929a6476f8ccc63.png)假设残余风险）。最优清仓听起来很适合![\mathbb{Q}](img/969ce5c634b2b4963929a6476f8ccc63.png)，但违反了风险中性，因为持仓者面临一个不完整的市场。这两个问题的实际解决方案取决于![\mathbb{P}](img/f2d0e071de256bbddee88d21a6582414.png)和![\mathbb​将这两个例子推广开来，这种收敛的![\mathbb{P}](img/f2d0e071de256bbddee88d21a6582414.png)——![\mathbb{Q}](img/969ce5c634b2b4963929a6476f8ccc63.png)世界的以下特征正在显现：

+   **现实生活中的![\mathbb{Q}](img/969ce5c634b2b4963929a6476f8ccc63.png)**：风险中性幻想消失，揭示了![\mathbb{P}](img/f2d0e071de256bbddee88d21a6582414.png)问题的混乱巢穴。

+   **![\mathbb{P}](img/f2d0e071de256bbddee88d21a6582414.png)形式化**：![\mathbb{P}](img/f2d0e071de256bbddee88d21a6582414.png)正在越来越多地被数学形式化，借鉴了来自![\mathbb{Q}](img/969ce5c634b2b4963929a6476f8ccc63.png)的模型和来自概率和统计学不同领域的理论。

+   **跨学科**：大型维度、形式化和校准的模型需要跨越![\mathbb{P}](img/f2d0e071de256bbddee88d21a6582414.png)、![\mathbb{Q}](img/969ce5c634b2b4963929a6476f8ccc63.png)和大规模机器学习的深厚跨学科知识。

+   **经验性**：在模拟复杂现实世界时，广泛采用的是经验统计和蒙特卡洛方法，而不是封闭形式的分布和证明。

+   **领导力**：统计学家和计算机科学家正在加速![\mathbb{P}](img/f2d0e071de256bbddee88d21a6582414.png)（数学家也在其中），正如物理学家对![\mathbb{Q}](img/969ce5c634b2b4963929a6476f8ccc63.png)所做的那样。

这种趋同代表了量化金融美好文艺复兴的潜力，为调和长期存在的技术矛盾提供了可以在实践中交易（而不是自我陶醉于风险）的解决方案。这种趋同世界中有多少策略具有真正的可扩展性，还有待回答。

向前看，阿尔法（alpha）将越来越多地倾向于那些理解并与此趋同进行交易的人。对于那些不理解的人，这将迅速演变成一种[结构套利](https://quantivity.wordpress.com/2011/08/28/fund-structure-arbitrage/)。
