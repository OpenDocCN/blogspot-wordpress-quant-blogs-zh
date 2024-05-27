<!--yml

类别：未分类

日期：2024 年 05 月 12 日 22:50:44

-->

# Falkenblog: Bad Data, Bad Theory, No Surprise

> 来源：[`falkenblog.blogspot.com/2008/10/bad-data-bad-theory-no-surprise.html#0001-01-01`](http://falkenblog.blogspot.com/2008/10/bad-data-bad-theory-no-surprise.html#0001-01-01)

So I'm reading a paper (

[经济灾难债券](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=995249)

by Coval, Jurek and Staffard) on how CDOs tranches are mispriced. Big publication in the

[美国经济评论](http://www.aeaweb.org/aer/contents/accepted.html)

。其中一个关键假设是，从实证上看，预期损失的收益率差会随着违约率的增加而增加，也就是说，垃圾债券的总收益率高于投资级债券；风险带来回报，等等。但是请考虑，美林高收益指数从 1987 年到 2008 年 9 月的年化收益率为 6.75％，而美林投资级指数的年化收益率为 6.49％。这是一个指数的回报率差异，未调整风险。加上交易成本，垃圾债券指数的回报低于投资级债券，然而学术界似乎对此毫不知情。

作者引用了两篇指出 AAA 和 BBB 利率之间差异的论文，并假定它延伸到垃圾债券（错误，不）。他们还引用了一篇文章

[Hull, Predescu and White](http://www.rotman.utoronto.ca/~hull/downloadablepublications/CreditSpreads.pdf)

(2005), who assert the B spread to Treasuries to be an average of 585 basis points. Bloomberg benchmark curves, and data I had at Moody's, would estimate a 405 basis points spread from 1991 to 2005, so I have no idea where they are getting their data. Hull et al mention Merrill, but I'm not sure which index. It's wrong.

无论如何，他们建立在糟糕的数据和一个（CAPM）在其他任何地方都不起作用的理论的精彩模型，并且令人震惊的是，它也与数据不符：

> 我们表明，参考投资级信用违约掉期指数的最高级别条款的损失主要与最坏的经济状态有关，这表明它们应该以比具有相同信用评级的单一名称债券更高的收益率差价交易。令人惊讶的是，这一推论事实上并不得到支持。

惊讶吗？在...的背景下

all

那个支持夏普-林特纳 CAPM 的数据（讽刺）？

但是，关于一个重要的问题——CDO 的本质是什么？——在金融研讨会上他们的快速介绍似乎从未提及垃圾债券中缺少风险溢价，这使得他们的论文的前提成为无效的论点。它可能存在什么潜在的不当激励？他们指出，AAA 级 CDO 比普通债券的 AAA 级更具周期性，但 AAA 级证券的相关性并不像其违约率点估计那样重要或有趣。他们得到了一个无关紧要的答案，即人们正在套利一种不存在的风险溢价。在许多方面，这完全是错误的：风险溢价不存在于 CDO（垃圾）或截段的抵押品中真正重要的地方；这些交易中的边际参与者是交易的股权所有者，而不是 AAA 级投资者；AAA 级 ABS 的收益高于纯粹的公司 AAA 评级债务，因此在这里的套利是不存在的（特别是因为 AAA 级 ABS 将需要一代人的时间才能再次获得真正的 AAA 级信誉）。

我并不是要如此批评——这是一个清晰的方法，看起来是合理的（尽管推断 0.7 的货币性不是）。只是错了。
