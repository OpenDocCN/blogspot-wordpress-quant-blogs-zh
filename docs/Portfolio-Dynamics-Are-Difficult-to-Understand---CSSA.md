<!--yml

category: 未分类

date: 2024-05-12 18:07:06

-->

# 投资组合动态难以理解 | CSSA

> 来源：[`cssanalytics.wordpress.com/2012/01/23/portfolio-dynamics-are-difficult-to-understand/#0001-01-01`](https://cssanalytics.wordpress.com/2012/01/23/portfolio-dynamics-are-difficult-to-understand/#0001-01-01)

“*一个投资组合的风险不是其组成部分向量的线性函数。相反，一个投资组合的方差是其组成的二次函数。这使得大多数分析师和投资者的直觉受挫。事实上，风险的本质可能是投资管理中使用定量分析的最重要论据。这个事实不能责怪投资者或分析师。哈里·马克维茨也不能。自然使风险成为一个二次函数。马克维茨只是发现了它*。” *威廉·夏普*

心理学家进行的研究一直在说明人类在正确整合多个信息源方面存在困难。即使因素可以合并成线性函数，法律和医学等不同领域的人类专家也无法像简单的回归模型那样表现良好。当处理凸函数或非线性问题时，这个问题尤其突出。威廉·夏普因将一个否则极具反直觉的二次解决方案（由哈里·马克维茨提出）简化为线性框架而获得了诺贝尔奖。这个模型被许多人称为 CAPM，不幸的是，这个模型需要太多的简化假设才能使其工作。后续研究表明，其中几个假设似乎在资本市场中不成立。最大的违约是假设β和未来回报（系统性风险）之间存在正期望的线性关系。实践中，研究表明，β要么呈负相关，要么与未来回报没有明确的关系，并显示出更多的非线性特征。

原始的马科维茨（MPT）框架非常难以概念化，并导致了本应不会出现的投资组合。存在几个违反直觉的属性，以下是两个有趣的属性：1）当大多数投资组合的夏普比率很高时，添加降低投资组合波动性的资产将增加夏普比率，而不管它们的回报如何；2）当大多数投资组合的夏普比率接近零时，添加具有正回报的资产将增加夏普比率，而不管它们的波动性如何。如果一个人使用判断力来形成投资组合，他们极有可能不会考虑到这些属性。这就是离散管理人员遇到麻烦的地方 - 他们可能很了解如何预测回报或生成可能的场景，但整合这些信息并不像看起来那样直截了当。这是投资组合数学发挥最大价值的地方。

尽管 MPT 有其优势，但理解数学可能出错的地方也同样重要。首先，这些缺陷主要源于估计噪声时间序列数据的困难以及生成“最优”解决方案时错误加剧的问题。MPT 优化可能会变得高度集中，不经意间最大化分配错误，这取决于输入的不稳定程度，如回报、相关性和波动性。然而，数学在功能上仍然是正确的，并且与多个回归模型背后的数学紧密相关。在下一篇文章中，我将展示不同的优化算法之间的关系。大多数算法有一个共同的主题，但在研究中并没有明确讨论。
