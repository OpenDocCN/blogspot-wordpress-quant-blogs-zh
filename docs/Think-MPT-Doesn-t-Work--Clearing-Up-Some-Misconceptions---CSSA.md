<!--yml

category: 未分类

date: 2024-05-12 17:46:13

-->

# 对 MPT 持怀疑态度？澄清一些误解 | CSSA

> 来源：[`cssanalytics.wordpress.com/2015/06/25/think-mpt-doesnt-work-clearing-up-some-misconceptions/#0001-01-01`](https://cssanalytics.wordpress.com/2015/06/25/think-mpt-doesnt-work-clearing-up-some-misconceptions/#0001-01-01)

***读者注意：** 我最近在 **[Blue Sky Asset Management](http://www.bsam.com/)** 上发布了一些有趣的材料，可能会引起兴趣。这包括我们对当前市场观察的月度评论，还有一系列关于动态资产配置的**[白皮书系列](http://www.bsam.com/research/)**，绝对值得一读。我最近还在网站上发布了一篇新的博客文章：[防守是最好的进攻](http://www.bsam.com/2015/06/19/1468/)。读者们应该密切关注我们的网站，因为我们计划在未来推出一些更“极客”的研究论文和有趣的当前市场分析。

我花了很多年时间研究不同的资产配置方法，包括传统和非传统投资组合优化的应用。鉴于近期博客圈对这个话题的热议，我觉得值得分享我的一点看法。将优化应用于战术方法可能是读者们已经熟悉的话题，我最近在 LinkedIn 上发布了一篇关于这个主题的文章：[对 MPT 持怀疑态度？你可能是在错误的方式下使用它](https://www.linkedin.com/pulse/think-mpt-doesnt-work-you-probably-using-wrong-way-david-varadi)。Flex Capital 的[Wouter Keller](http://www.researchgate.net/profile/Wouter_J_Keller)，BPG 的 Adam Butler（[BPG](http://bpgassociates.com/)），以及 Quantstratrader 的 Ilya Kipnis（[Quantstratrader](https://quantstrattrader.wordpress.com/)）合著了一篇很棒的论文，在我的文章中引用过，鼓励读者们去看一看：[动量和马科维茨；黄金组合](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=2606884)。他们指出，在动态环境中使用 MPT 算法结合短期数据有助于捕捉动量效应，并产生具有良好风险调整回报的多样化投资组合。这篇论文在很多方面是对一个研究和从业者辩论流的重要贡献，有时候这个流是不平衡和片面的——而且没有好的逻辑理由。MPT 在行业中被广泛和一致地批评，因为人们认为它存在算法特定的缺陷，以及显示出糟糕的样本外表现的研究。当然，这主要是因为它被错误地使用——在中间或较长的时间跨度上，这是不适合这种方法的。同样重要的是要记住，行业巨头如 AQR 和高盛已经使用动态 MPT 方法的变体构建了表现非常好的复杂投资组合几十年了。

与同一主题相关的其他一些非常有趣的文章还包括[Logical Invest](http://logical-invest.com/)的 Frank Grossman 撰写的[普遍投资策略](http://seekingalpha.com/article/2714185-the-spy-tlt-universal-investment-strategy)以及[Newfound Research](http://blog.thinknewfound.com/)的 Andrew Gogerty 撰写的[动量与多元化](http://blog.thinknewfound.com/2015/05/momentum-diversification-powerful-risk-adjusted-combination/)——这篇文章获得了声望显赫的[NAAIM Wagner 奖](http://www.naaim.org/resources/wagner-award-papers/)的第三名。这两篇文章中用于优化的方法几乎相同。它们都通过蛮力将带有约束的选择集合的股指曲线组合成投资组合，而不是使用 MPT，从而找到最大的夏普比率。重要的是要理解，在大多数情况下，MPT 和这些方法实际上是等效的（MPT 通过数学方式找到蛮力最优解）。Grossman 在目标函数中使用了一个带有风险厌恶参数的变体。Newfound 引入了一个变化，允许在回顾窗口中使用不同的再平衡窗口，这更类似于动态规划方法。在这两种情况下，我都想向读者澄清，通过组合股指曲线（假设每日再平衡）找到夏普比率与使用计算出的相关性/波动性和回报来计算夏普最优投资组合是相同的——所以无法避免“估计误差”，它只是隐含而不是显式。

Wes Gray of [Alpha Architect](http://www.alphaarchitect.com/) 总是很好的研究来源，并在其文章中展示了在资产配置中对 MPT（而非战术）的更传统使用；[小心那些带着公式的极客们](http://blog.alphaarchitect.com/2015/05/19/tactical-asset-allocation-beware-geeks-bearing-formulas/)。不幸的是，这篇文章并没有对比苹果和苹果，因为与所比较的简单战术基准相比，MPT 回顾参数的期限更长。因此，这篇文章恰好对动态格式中使用 MPT 的做法不利，这在行业内很常见，在我看来这有点不公平，因为可以工作的东西比不好的东西要多。恰好使用 MPT 进行战术格式操作会带来一套独特的复杂性，而这些并不会困扰更简单的方法——这包括更高的换手率，更集中的投资组合以及对估计误差更大的敏感性。估计误差更高的原因有几个。一个是维度更大，因为有更多需要估计的输入。另一个是，在 MPT 中，回报的幅度决定了权重，以及回报的排名——相比之下，基本动量方法只关注排名。这使得与简单动量方法相比，MPT 中的回报估计承受更大的压力。另一个问题是整合噪声/随机相关性，这会干扰回报估计的误差。增加相关性对于强调多样化很重要，但仅限于它们不是高度错误 prone 的程度。使用 MPT 进行投资策略分配，而不是资产配置，甚至更具挑战性，因为策略具有更多复杂的输入需要估计，而且有些输入无法定量估计。积极的一面是，与使用规则构建的简单战术系统相比，使用 MPT 进行战术方法携带的数据挖掘偏见要小得多。如果系统构建者可以自由变化多个参数，并且可能还通过反复测试选择他们的投资宇宙，这尤其正确。使用像 MPT 这样数学紧凑的一个算法，带有一个回顾参数，受到这些隐蔽的数据挖掘问题的影响要小得多。

我认为行业内辩论的最重要收获是，许多算法、交易方法或指标往往因为不恰当或不合适的分析（或使用）而被不公平地抛弃，而不是因为真正的不足。技艺高超的厨师可以用几种普通或新奇的食材创造出杰作，而知识有限的厨师可能会认为同样的食材盒子完全不适合制作一顿合适的餐点。即使采用终极的黑盒机器学习方法，也有许多人取得了成功——这是一条充满危险的道路，就像攀登珠穆朗玛峰一样，但显然有一些好的攀登者（参见文艺复兴科技公司）。当然，在良好的定量系统设计中，就像烹饪一样，使用好的简单食材可以轻松地创造出一顿美餐，而无需太多的操纵或努力。通过探索更奇异的应用来推动边界，虽然失败的风险更大，但机会也更大，这在高度竞争的市场中是值得冒险的。你只需要很好地理解如何划清界限。***在一定程度上，我猜将 MPT 纳入战术资产配置的决定讽刺地成为一个关于效用曲线的……问题。***
