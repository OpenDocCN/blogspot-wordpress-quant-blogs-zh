<!--yml

分类：未分类

日期：2024-05-18 07:04:04

】

# 物理视角：为什么博弈论常常是无效的...

> 来源：[`physicsoffinance.blogspot.com/2011/10/why-game-theory-is-often-useless.html#0001-01-01`](http://physicsoffinance.blogspot.com/2011/10/why-game-theory-is-often-useless.html#0001-01-01)

经济学非常依赖于均衡的概念。这在任何竞争均衡模型中都是真的——探讨交换如何在原则上导致资源的最优分配——或者更一般地说，在博弈论的背景下，探讨战略游戏中的稳定纳什均衡。

物理学家在两种情况下对均衡感到完全不满的是，经济学家几乎完全忽视了关键问题，即模型中的代理商是否有可能合理地

寻找

一个均衡。你可以假设完全理性的代理商并证明均衡的存在，但这可能是一个无关的数学练习。具有有限推理能力的有现实感的代理商可能永远无法通过学习达到这样的解决方案。

更有可能的是，在许多情况下，不太完全理性的代理商，即使他们在学习方面非常聪明，也可能永远找不到一个整洁的纳什均衡解决方案，而是继续变化、适应和相互响应，导致持续的混乱。天真地看，这在任何情况下似乎尤其可能——想想金融市场，或者整个任何经济——其中可能的策略数量巨大，而且通过完美的理性反思“解决问题” simply impossible（没有人通过计算纳什均衡来下棋）。

这个洞察力的精彩说明来自于

【一篇新论文](http://arxiv.org/PS_cache/arxiv/pdf/1109/1109.4250v1.pdf)

由托拜厄斯·加拉和道恩·法默撰写。这是我所看到的第一个（尽管可能还有很多其他）研究，它以一种通用的方法探讨了复杂、高维游戏中均衡的相关性。这个结论和它的直观合理性一样重要：

> 在这里我们展示，如果玩家使用标准的学习方法，对于复杂游戏，存在一个很大的参数范围，在其中人们应该预期复杂的动态。这意味着玩家从未收敛到一个固定的策略。相反，他们的策略随着每个玩家对过去条件作出反应并试图比其他玩家做得更好而不断变化。策略空间中的轨迹表现出高维混沌，这表明在大多数意图和目的上，行为本质上是随机的，未来的演变是固有不可预测的。

换句话说，在足够复杂的游戏中，来自平衡分析的洞察力并不能告诉你很多。如果代理商以一种合理的方式学习，他们根本找不到任何平衡，而战略行为的演变 simply carries on indefinitely. 系统保持在非平衡状态。

稍微详细一点。他们的基本方法是考虑两个玩家之间的一般游戏，比如说，爱丽丝和鲍勃。让两个玩家各有 N 种可能的策略可以选择。任何此类游戏的支付矩阵都是 NxN 矩阵（每个玩家一个）给出他们对于每对策略的支付。这种分析中的巧妙想法是随机选择游戏，通过从以零为中心的正态分布中选择爱丽丝和鲍勃的支付矩阵元素。作者简单地选择一个游戏并通过模拟两个玩家通过经验学习 -- 如果那些策略取得好的结果，他们就会更频繁地从他们 N 种可能性中选择策略。

当 N = 50 时，结果显示清楚地表明许多游戏从未进入任何稳定的行为。相反，从未找到平衡。典型的动态体现在下面的图表中，该图表显示了两个玩家（爱丽丝的 - 鲍勃的）收益随时间的变化。即使两个代理商努力学习最佳策略，游戏的复杂性也阻止了他们的成功，而且游戏没有丝毫稳定下来的迹象：

![图](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhbT4z12BUjqXYlAhvu4YXxDKxT4Uaz8aQeDa5pOBOOrB6GEgytyDe4gXJKstaBY3XBHLRKMsd9MPElJZatiM67QiA0ANkW11tRMzGinClIUlu4Aj9CLl6MZuEJUBJ09tDfEbEJiv9q_yO8/s1600/galla_farmer_fig.png)

正如作者所指出的，这种丰富、复杂、持续的动态与人们在现实系统中看到的动态非常相似，例如金融市场（上面的时间序列显示了聚集波动，市场波动也是如此）。有相对平静的时期，被极端波动的发作打断。然而这里没有任何干预 -- 没有“冲击”系统 -- 会产生这些变化。所有这些都来自完全自然的内部动态。而且这在 N = 50 策略的游戏中。如果 N 大于 50，如在现实世界中，或者如果玩家数量超过两个，事情可能会变得更加混乱，并且不太可能稳定下来。

因此，我认为这实际上是相当深刻地表明了来自博弈论的平衡分析在复杂现实世界设置中的可能不相关性。动态真的很重要，不能被理论化为不存在，无论经济学家们如何努力尝试。正如论文总结：

> 我们的结果显示，在许多情况下，放弃经典博弈理论的工具而选择动态系统的工具更有用。它还表明，许多已经引起相当兴趣的行为，比如金融市场中的聚类波动性，可能仅仅是高度通用现象的具体例子，并且应该预期会在各种不同的情况下发生。
