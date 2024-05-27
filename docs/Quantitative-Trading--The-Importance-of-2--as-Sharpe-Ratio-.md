<!--yml

category: 未分类

日期：2024-05-12 19:00:13

-->

# 量化交易：2 的重要性（作为夏普比率）

> 来源：[`epchan.blogspot.com/2012/11/the-importance-of-2-as-sharpe-ratio.html#0001-01-01`](http://epchan.blogspot.com/2012/11/the-importance-of-2-as-sharpe-ratio.html#0001-01-01)

一位读者

[ezbentley](http://epchan.blogspot.com/2010/04/how-do-you-limit-drawdown-using-kelly.html?showComment=1352433899601#c2233375091631222369)

最近指出了一个在

[推导](http://www.edwardothorp.com/sitebuildercontent/sitebuilderfiles/KellyCriterion2007.pdf)

凯利公式的：如果我们应用最优的凯利杠杆，那么年化的标准差

*compounded*

你的权益的增长率不是别的，正是夏普比率（Sdev=S）。这个事实本身是有趣的，但它的含义与行为金融学的另一个有趣事实相关，所以我将在这里重现我们的讨论。

假设我们的策略有一个年化的夏普比率为 2。根据上述结果，Sdev 也等于 2。这可能会让一些人感到惊讶：我们的复合增长率 g 的 200%的标准差 - 难道崩溃的可能性不是很大吗？但是看看 g 本身：g=S²/2，所以当 S=2 时，g 本身正好是 200%。这里的 Sdev 为 200%意味着，如果增长率在其平均值下降一个标准差以下，我们仍然可以在这一年 manage not to lose money。另一种说法是，基于高斯分布，我们有 84.1%的机会使我们的年回报率大于 0。

如果 S 超过 2，情况会更好。例如，当 S=3 时，g=4.5，但 Sdev 仅为 3。所以你可以看到，当 S 超过 2 时，g 的一个 1 标准差的波动低于平均值仍然可以得到一个正数：年度盈利。

这是一个非常有趣的结果：这意味着 S=2 真的是比我意识到的更多的方面的重要阈值。从行为金融实验中，我们已经知道人类要求$2 的利润来承担$1 的风险。考虑到组合经理普遍希望在当年不亏损，结果表明至少 2 的夏普比率的的需求是非常理性的！

===

现在，是时候宣布两项公共服务了：

1) 那些寻找将 Matlab 连接到 Interactive Brokers 方法的人应该查看

[undocumentedmatlab.com](http://undocumentedmatlab.com/ib-matlab/)

该产品的创作者有一本配套书籍，该产品的文档非常出色。

2)

[NAG](http://www.nag.com/numeric/MB/manual64_23_1/pdf/GENINT/product.html)

销售高性能的 Matlab 工具箱，供那些喜欢使用替代原生的那些人使用。

3)

[在此](https://twitter.com/FIXGlobalOnline)

这是 FIXGlobal Online 的 Twitter 信息流，该杂志是由 FIX 协议的创作者所创建的，这是一种订单提交标准。来自全球金融界的有趣新闻。
