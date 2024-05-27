<!--yml

类别：未分类

日期：2024-05-12 20:29:31

-->

# Falkenblog：最小波动率投资组合策略

> 来源：[`falkenblog.blogspot.com/2012/05/minimum-volatility-portfolio-tactics.html#0001-01-01`](http://falkenblog.blogspot.com/2012/05/minimum-volatility-portfolio-tactics.html#0001-01-01)

MSCI 在创建指数方面非常在行，他们的

[全球最小波动率指数](http://www.msci.com/products/indices/strategy/risk_premia/minimum_volatility/)

很有趣（BB 代码 M00IWO$P）。如果我将其收益与简单平均值相比

[我的最小方差投资组合](http://www.betaarbitrage.com/)

绘制自 UKX、NKY、MSER 和 SPX 指数（英国、日本、欧洲、美国）的数据。它们非常匹配。在我获得的 MSCI 全球最小波动率数据的时间段内，平均收益和标准差基本相同。

我的指数是通过每隔 6 个月选取这些主要指数的所有成分，并应用一种优化算法，使用前一年的每日数据来最小化方差得到的。解决方案确定了接下来 6 个月的一组固定权重。MSCI 更全球化地权衡各种因素，并有 8 个不同的约束条件。看起来，如果你只想要一个全球最小方差，那些关于行业等的小限制在风险/回报效应上并不是那么重要。这凸显出这个问题在某种程度上有一个“平坦的最大值”，即在某一层面上距离不太接近的解决方案在最终答案上实际上非常接近。参见罗宾·多斯的

[不当线性模型的坚固之美](http://heatherlench.com/wp-content/uploads/2008/07/dawes2.pdf)

更多关于这一现象的信息（奇怪的是，这个标题的谷歌搜索结果的第一页是

[1995 年发行的音乐 CD](http://www.discogs.com/Chris-Stamey-and-Kirk-Ross-The-Robust-Beauty-Of-Improper-Linear-Models-In-Decision-Making/release/401743)

。我猜这些艺术家是在讽刺）。

任何低波动率策略的真正增值不在于它们的低波动率算法，而在于对如何看待诸如特异波动率、规模、动量和价值等互补因素的战略决策。这里的一切都是相关的，因此默认忽视这些因素是不可能的。重要的细节取决于对这些因素如何相互作用的假设：因子收益是相互抵消还是相互叠加，这个答案取决于你如何看待这些因素，比如

[特征而不是潜在风险因子](http://seekingalpha.com/article/309986-identifying-portfolio-risk-characteristics-vs-factors)

。
