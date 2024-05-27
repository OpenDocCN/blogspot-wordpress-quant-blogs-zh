<!--yml

类别：未分类

日期：2024-05-18 13:48:43

-->

# Optimal 10b5-1 Monetization | Quantivity

> 来源：[`quantivity.wordpress.com/2011/09/27/optimal-10b51-equity-monetization/#0001-01-01`](https://quantivity.wordpress.com/2011/09/27/optimal-10b51-equity-monetization/#0001-01-01)

随着 IPO 交易量的增加，读者们纷纷私下询问关于符合[10b5-1](http://en.wikipedia.org/wiki/SEC_Rule_10b5-1)规则的股票/股票期权/限制性股票（ESO/RSU）货币化计划的*实用算法*，这受到了最近关于[最优股票货币化](https://quantivity.wordpress.com/2011/07/30/optimal-equity-monetization/)的三篇理论系列文章的启发。这个话题值得探讨，先前的免责声明是仅供信息参考：

+   *微观宇宙*：这个话题是交易的微观宇宙，因为它包含了许多常见问题。

+   **重要性**：选择计划可以说是影响一生的最重要的财务决策。

+   *现实生活中的量化分析师*：理论撞上金融服务行业零售投资者的复杂性

+   *Greenfield*: 有关这个主题的文献很少，并且与现实实践脱节。

+   **异国情调**：可以说是最普遍的零售异国产品（exotic）的说明性例子

本文将探讨一种新的*10b5-1 计划货币化模型*，该模型符合美国证券交易委员会（SEC）的规定，并且与经纪对手方施加的共同实践限制兼容。由于其范围不小，这个模型和相应的背景将在几篇帖子中分部分介绍。

本文首先通过直觉来阐述模型，然后简要回顾现有文献。第二篇文章将描述该模型，提供实用的 R 代码，并通过将其应用于一个代表性的股票来生成结果。对于熟悉投资组合优化的人来说，这个模型让人想起[Black-Litterman](http://en.wikipedia.org/wiki/Black%E2%80%93Litterman_model)模型，因为它依赖于对基础股票的“观点”。

**停止标准**

直观地，一个计划的优化性可以通过计划内外的交易利润差异来衡量。换句话说，评估计划的基准是如果没有计划，持有人的情况会怎样。这是有道理的，因为计划实际上充当了一种交易约束（一种*投资组合约束*），因为所有交易的执行规则都必须提前指定。

一种简化的方法是预测：猜测股价的演变，并构建一个最大化相应利润的计划。这种方法只对一类持有人有效：那些认为股票将崩盘的人；对他们来说，计划很简单：以市场价格尽可能多地、快速地卖出。

对于其他人来说，预测方法相当简单：在无限多的潜在股价路径中，什么理由选择一条路径？在没有预知能力的情况下，另一种选择是使用[最优停止](http://en.wikipedia.org/wiki/Optimal_stopping)和[最优控制](http://en.wikipedia.org/wiki/Optimal_control)（参见费格逊的[最优停止及其应用](http://www.math.ucla.edu/~tom/Stopping/Contents.html)，这是一个简洁的理论介绍）。

即，*将股价建模为随机过程，并将问题表达为在每个要货币化的股票过程中进行最优停止*。虽然不一定是一个[马尔可夫过程](http://en.wikipedia.org/wiki/Martingale_%28probability_theory%29)，但考虑到持有人在观察过程的任何实现之前必须决定计划，这个过程可以被假设为一个马尔可夫过程。此外，这个模型定义在真实概率测度![\mathbb{P}](img/f2d0e071de256bbddee88d21a6582414.png)（不是风险中性测度![\mathbb{Q}](img/969ce5c634b2b4963929a6476f8ccc63.png)），因为由于对卖空和交易衍生品的有法律限制，持有人在市场上面临的是*不完整*的。

在深入数学和代码之前，让我们首先假设有这样一种最优计划算法的属性：

+   *可执行*：对手方必须愿意执行计划

+   *盈利最大化*：最大化货币化盈利

+   *时间最小化*：最小化货币化所需的时间

+   *灵活风险*：能够根据不同的风险承受能力适应货币化

+   *动态*：在一段时间范围内最优，而不仅仅是计划初始时

+   *适应性*：根据当前市场条件适应性地调整货币化

+   *无效用*：不依赖于不可观察的效用函数

虽然听起来可能很显然，但找到满足这些属性的模型却出奇地具有挑战性。实际上，文献中没有一个模型同时具备这些属性。

**实用文献综述**

由于这个模型的意图是*实用实施*，所以文献综述将采取实用主义的视角。简而言之，文献资料稀少，缺乏实用例子，且作者是一些明显不熟悉货币化现实的善意学术人士。从[数量研究人士](https://quantivity.wordpress.com/2011/03/06/people-of-quant-research/)，唯一两个主要研究包括执行股票期权的学者是[亨德森](http://www.oxford-man.ox.ac.uk/people/members_henderson.html)和[卡彭特](http://people.stern.nyu.edu/jcarpen0/); 从会计界，[雅戈林泽](http://leeds-faculty.colorado.edu/alja4277/10b5_1.html)也在做很好的工作（如果你知道其他的，请留言）。

有一点历史背景是有帮助的：在 2000 年之前，由于担心无法提供足够的积极防御 against 内部交易，研究货币化的广泛做法几乎是不可能的，因为没有人愿意谈论这个问题。因此，货币化实践分为两派：大众在公开窗口中交易特质风险，而更复杂的人则通过 OTC 策略执行名义金额（主要是[PVFs](http://en.wikipedia.org/wiki/Variable_prepaid_forward_contract)和[ZCCs](http://en.wikipedia.org/wiki/Collar_%28finance%29)）。2000 年，随着[10b5-1](http://en.wikipedia.org/wiki/SEC_Rule_10b5-1)的颁布，为通过预先指定的*机械*计划进行的交易提供了积极防御。因此，货币化的现代时代开始了，与量化金融和算法交易有着明显的联系。

十多年后，文献研究终于开始关注*货币化的风格化事实*（例如看似次优的期权行权、交叉对冲、合同义务、终止风险、批量行权和经纪人约束/成本）。例如，[梁](http://www.ieor.columbia.edu/fac-bios/leung/faculty.html)在他的 2011 年文章《员工股票期权：最优对冲、次优行权和合同限制的会计处理》[Employee Stock Options: Accounting for Optimal Hedging, Suboptimal Exercises, and Contractual Restrictions](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1290404)中，首次系统地调查了这些风格化事实。其他试图探究这一问题的文章，按洞见程度递减排列：

+   [高管股票期权的早期行权与公司未来的系统风险及特质风险](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1466246)，作者：Srivastava（2011）

+   [在员工股票期权估值中考虑风险规避、期权归属、工作终止风险和多次行权](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=943926)，作者：Leung 和 Sircar（2009）

+   [员工股票期权行权率的估计及对公司成本的影响](http://pages.stern.nyu.edu/~jcarpen0/pdfs/CarpenterStantonWallace2.pdf)，作者：Carpenter, Stanton 和 Wallace（2011）

+   [高管股票期权的最优行权及对公司成本的影响](http://people.stern.nyu.edu/jcarpen0/pdfs/CarpenterStantonWallace1.pdf)，作者：Carpenter, Stanton 和 Wallace（2010）

+   [风险规避与高管股票期权的批量行权](http://ideas.repec.org/a/eee/dyncon/v33y2009i1p109-127.html)，作者：Grasselli 和 Henderson（2009）

+   [员工股票期权的行权：一项实证分析](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=6072)，作者：Huddart 和 Lang（1996）

+   [高管人员通过风险多样化对员工股票期权早期行权的影响](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=294900)，作者：Hemmer, Shevlin 和 Matsunaga（1996）

+   [高管股票期权的行权与估值](http://people.stern.nyu.edu/jcarpen0/pdfs/Carpenter1998.pdf)，作者：Carpenter（1998）

与调查风格事实并行，一个重要的理论洞察被发现：*最优停止理论可以应用于股票期权行使*（从而实现货币化，在大量情况下）。毫无疑问是偶然的，人们偶然发现了精确描述“正常”人寻求货币化的心理模型的数学；经典的 ![\mathbb{P}](img/f2d0e071de256bbddee88d21a6582414.png) 思维（个体主义持续时间在 ![\mathbb{Q}](img/969ce5c634b2b4963929a6476f8ccc63.png) 中不起作用）。

这一见解在 Leung、Henderson（与 [Hobson](http://www2.warwick.ac.uk/fac/sci/statistics/staff/academic-research/hobson/) 合作）和 Carpenter 的多篇论文中得到了体现。也许并非巧合的是，Leung 来自工业工程（显然，金融和运营研究的人员偶尔也会交谈）。虽然这些论文提供了一些见解，但它们的基本实用缺陷是过于依赖效用函数（尽管很好地实践了[前景理论](http://en.wikipedia.org/wiki/Prospect_theory)），因此形式化到实际无用的程度：

然而，尽管采用了最优停止模型，这些文章很快得出了与许多“正常”人的直觉相冲突的结果。例如，来自 Henderson 和 Hobson（2011）的第 2 页：

> 最优行使策略是门槛形式的——代理人应该在资产价格首次达到依赖于尚未行使的那部分投资组合的门槛水平时行使期权。行使足够的期权以保持投资组合持有量低于门槛，因此解决方案是单一定制控制。

这种说法 arguably 引发了质疑，即通过假设一个门槛阈值触发模型。甚至更不实用的是时间同质性的假设（第 8 页），因此也是时间独立的（第 7 页）：

> 在给定价格水平下，最优的选择不是行使期权，那么在没有任何中间期间行使过期权的情况下，如果价格回到这个水平，仍然最优的选择是不行使期权。

这在实际中显然是没有意义的，因为它承认了期权可能永远不受货币化的解决方案（即超过门槛的）。更实用的是，时间同质性应该是 *[内生](http://en.wikipedia.org/wiki/Endogenous)* 的：偏好的时间等价是由个体的风险规避决定的。风险承受能力低的人会在价格达到门槛时立即货币化（或者在极端情况下，无论门槛如何都货币化）。相比之下，风险承受能力较高的人可能更愿意货币化一定比例，然后等待一段时间来看价格如何演变。

先前的最优控制洞察建立在概率论的一个小但有趣的研究线索上，该线索由以下文章代表：

最后，以下文章认识到货币化*不一定是一个单期问题*，因此引入了多个停止时间：

然而，尽管有这么多优秀的文献，一个有效的实用货币化模型尚未出现。
