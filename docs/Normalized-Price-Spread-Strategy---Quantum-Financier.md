<!--yml

category: 未分类

date: 2024-05-18 14:04:05

-->

# Normalized Price Spread Strategy – Quantum Financier

> 来源：[`quantumfinancier.wordpress.com/2010/06/17/normalized-price-spread-strategy/#0001-01-01`](https://quantumfinancier.wordpress.com/2010/06/17/normalized-price-spread-strategy/#0001-01-01)

这里是我最近几天想到的一个快速想法。我正在阅读有关统计套利和配对交易的内容，正如你们中的一些人可能知道，价差在领域中相当关键。配对交易背后的想法相当简单；找到表现相似的资产，然后当价差离开平均值时赌其回归正常。简单，优雅，仅基于直觉，这是我喜欢的一个交易概念的所有要素。

我研究了如何将这个概念融入一个简单的系统。这个策略关注的是收盘价与短期移动平均（本例中为 3 天）之间的标准化价差（差异）。换句话说，我使用最后收盘价与单一资产的 3 天移动平均之间的百分比排名函数。如果小于 50 百分位则做多，否则做空。以下是自 2000 年以来 SPY 的表现。

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/06/norm-spread.png)

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/06/norm-spread-result.png)

从概念上讲，这是很有道理的。如果最近的价格显示出强劲的相对强度，我们预计它会回归正常，相对强度较弱的情况则相反。标准化价差给了我们一个近期价格与过去几天以及平均值之间的偏差程度的指示，从这里我们可以预计一定程度的均值回归。如果价格变得“拉伸”，那么我会比价格在平均值附近波动时更有信心。话说回来，这个想法并没有什么天才之处；它只是另一个相对强度策略，与众所周知的 z-score 非常相似。然而，我喜欢使用百分位数，因为我们不需要假设任何分布，从而放宽了对数据正态性的需求。它还促进了基于信心的投注方案或 MarketSci 式的[“调光方法”](http://marketsci.wordpress.com/2010/05/12/tweaking-the-sector-rotation-strategy-part-2/)的创建。无论如何，我认为价差的概念是一个好概念，预计它会在博客上再次出现，因为我正在了解更多关于它的信息。

QF
