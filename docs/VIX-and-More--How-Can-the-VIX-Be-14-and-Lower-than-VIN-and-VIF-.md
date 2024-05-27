<!--yml

分类：未分类

日期：2024-05-18 16:25:32

-->

# VIX and More: VIX 可以为 14 且低于 VIN 和 VIF 吗？

> 来源：[`vixandmore.blogspot.com/2012/08/how-can-vix-be-14-and-lower-than-vin.html#0001-01-01`](http://vixandmore.blogspot.com/2012/08/how-can-vix-be-14-and-lower-than-vin.html#0001-01-01)

今天，许多初学者和高级 VIX 追随者都在猜想，为什么 VIX 下跌超过 5%，在 14.00 水平徘徊，当 SPX 下跌 0.4%且所有主要市场平均水平均大幅下跌时。更认真的 VIX 学生还将注意到，这次 VIX 下跌是在一个星期一，而典型的 VIX“[日历回归](http://vixandmore.blogspot.com/search/label/calendar%20reversion)”通常会导致波动性指数上涨约 1%。

大多数这些问题的答案都在于 VIX 的另一个特殊之处：卷积。直接引用自[CBOE 波动率指数（VIX）白皮书](http://www.cboe.com/micro/vix/vixwhite.pdf)，我们从第 4 页和第 9 页摘录到了以下两个重要的观点，我已将其按顺序呈现以便更容易理解：

> *“VIX 的组成部分是近期和次近期的认沽和认购期权，通常是第一个和第二个 SPX 合约月份。‘近期’期权必须至少剩余一周到期；这一要求旨在最大程度地减少靠近到期时可能发生的价格异常情况。当近期期权剩余时间少于一周时，VIX 将‘卷积’到第二个和第三个 SPX 合约月份。例如，在 6 月的第二个星期五，VIX 将使用在 6 月和 7 月到期的 SPX 期权进行计算。在接下来的星期一，7 月将取代 6 月成为‘近期’，8 月将取代 7 月成为‘次近期’。”*
> 
> *“在 VIX‘卷积’时，近期和次近期期权到期日都超过 30 天。使用的计算公式与计算 30 天加权平均值相同，但结果是σ² 1 和σ² 2 的外推；即，权重总和仍为 1，但近期权重大于 1，**次近期权重为负**（例如，1.25 和-0.25）。* [强调添加]

*当我首次在 2011 年 3 月发表有关[VIN](http://vixandmore.blogspot.com/search/label/VIN)和[VIF](http://vixandmore.blogspot.com/search/label/VIF)的文章时（[VIN，VIF 和一个过时的 VIX](http://vixandmore.blogspot.com/2011/03/vin-vif-and-obsolete-vix.html)），我惊讶地发现有多少投资者，包括精明和经验丰富的 VIX 迷，完全不知道这些指数。当时，芝加哥期权交易所甚至没有在其网站上提及 VIN 和 VIF，但他们后来为这两个指数添加了一个[引人注目的页面](http://www.cboe.com/micro/vin/)，并附上以下简短的评论：

> *CBOE 维护了跟踪从单一 SPX 到期日的隐含波动率水平的指数。*
> 
> *标记 VIN（彭博上的 VINX）- 用于 VIX 计算的较近期的 SPX 到期日*
> 
> *代码 VIF – VIX 计算中使用的较远期 SPX 到期日*

回到期权的滚动，今天 SPX 期权合约的月份向前滚动了一个月，因此较近期的月份（VIN）从八月移到了九月，较远期的月份（VIF）从九月移到了十月。更重要的是，根据上面引用的 VIX 白皮书中的加粗文本，今天的 VIX 计算包括了 VIN 的超过 100%以及 VIF 的***负数***。这就是 VIX 小于其计算中所用的两个组成部分（VIN 和 VIF）的原因。总之，VIN 和 VIF 之间的差异越大（现在这个差异是一个非常大的 9.4%），VIX 在 VIX 滚动后大幅下跌的可能性就越大。另外，随着我们接近 8 月 22 日 VIX 期权的到期日，VIX 计算中使用的负 VIF 成分的扭曲应该逐渐减小，因为 VIF 的权重将趋近于零，然后变为正数。

对于那些想要深入了解 VIX 计算细微差别的人来说，CBOE 的 VIX 白皮书是开始研究的最佳起点；下方的链接可能也会提供额外的见解。

相关文章：

***披露：*** *在撰写本文时持有 VIX*
