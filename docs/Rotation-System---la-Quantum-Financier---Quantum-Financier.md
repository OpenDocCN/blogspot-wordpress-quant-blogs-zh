<!--yml

category: 未分类

date: 2024-05-18 14:01:38

-->

# 量子金融家的轮动系统——量子金融家

> 来源：[`quantumfinancier.wordpress.com/2010/11/11/rotation-system-a-la-quantum-financier/#0001-01-01`](https://quantumfinancier.wordpress.com/2010/11/11/rotation-system-a-la-quantum-financier/#0001-01-01)

轮动系统最近产生了大量的虚拟墨水，例如 CSS Analytics [在这里](http://cssanalytics.wordpress.com/2010/02/23/rotation-concepts/)，Engineering Returns [在这里](http://engineering-returns.com/2010/07/23/rotational-trading-a-simple-but-powerful-concept-part-i-ii/)，然后是 MarketSci [在这里](http://marketsci.wordpress.com/2010/10/20/roundup-tactical-asset-allocation/)，这些都是几个例子。我最近一直在尝试这个概念，但采用了一种非常不同的方法。我觉得读者可能会对另一个解决类似问题的方法感兴趣。

Rotation systems are often based on two very simple concepts: momentum (relative strength) effect and negative correlation. The goal of such models is usually to allocate capital to securities trending on the upside. By selecting securities that are show negatively correlated behaviour we expect the securities to complement each other depending on the regime. For example one could include in the basket of available securities stocks and fixed incomes ETFs with the expectation to be long bond when stocks are not performing and vice-versa. This kind of model basically surfs the beta with the momentum of securities. This approach demands certain considerations when creating the model, and depending on the investor, various degrees of fancy maths are going to be used. When looking at creating such systems, we need to determine the following amongst others:

**1. 有哪些证券可用以及是如何选择的？**

资产之间的负相关性是这里的一个有吸引力的特征。我们也许还可以包含不同程度杠杆的 ETFs，以便在适当的时候积极增加 beta。然后，我们可以根据启发式方法、宏观经济关系、数据挖掘等来选择它们。

**2. 动量是如何测量和排名的？** 可以使用不同时间框架之间价格的简单标准化差异，或者使用变化率指标。RSI，[DVO](http://cssanalytics.wordpress.com/2009/07/29/the-dvo/) 或 [TSI](http://engineering-returns.com/tsi/) 指标也是不错的选择。或者，您可以拟合一个最小二乘模型，并评估斜率和残差。您还可以进行某种因子分解，创建一个因子模型来预测动量。

**3. 我们如何分配资本到不同的证券上？** 可以使用简单的等额现金头寸，或者我们可以利用波动性来调整证券之间的权重。经过某些调整后的均值-方差优化可能是一个不错的选择。

**4. 我们多久重新调整一次策略？** 大多数 TAA 系统每月重新调整一次，而一些轮动系统则是按周的时间框架进行交易。关键是要在仍能利用选定证券的上行趋势的同时最小化交易成本，并缓解回撤。这类系统的吸引力通常在于它们的风险调整后的表现，我们不希望妥协这一点。

**5. 我们在系统中考虑过替代/创新的指标吗？** Marketsci 的 Michael 最近谈到了在市场冲击期间考虑相关性的做法。这种创新方法对他来说似乎非常有效，而且这里真的只有天空是极限。我们只需要平衡复杂性和质量。

在不泄露下篇文章内容的前提下，我可以说明我的轮动系统将与其他博客上讨论的内容（至少我所知道的）非常不同。我们不是使用历史相对强度，而是看看如何使用机器学习分类来选择证券并预测。我还将尝试整合新的指标以帮助提高系统性能。

QF
