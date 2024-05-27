<!--yml

类别：未分类

日期：2024-05-18 15:10:30

-->

# 及时投资组合：回撤是系统成功的最大决定因素吗？

> 来源：[`timelyportfolio.blogspot.com/2011/12/is-drawdown-biggest-determinant-of.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/12/is-drawdown-biggest-determinant-of.html#0001-01-01)

在我所有的系统开发中，我仍然无法确定哪些普遍的基础条件能显著提高一个系统超越买入并持有的概率。此外，我找到的讨论也非常少，所以也许 R 语言加上 ttrTests 的帮助能回答我何时应该仅仅买入并持有（这对于资金经理来说是一个非常愉快的情况）。自 1998 年进入这个行业以来，我经常说，我梦想着有一天我可以仅仅买入并持有，就像 1980-1990 年代的日本股票，1990-2000 年代的美国股票，以及 1982 年至今的美国债券一样。

那些关注我的博客或了解我的人已经理解了我对回撤的迷恋，但这种迷恋更多地集中在客户/经理心理学上[（长期投资）](http://ssrn.com/abstract=1958258)而不是回撤对战术系统的影响上。我不理解行业对标准差的关注。我从未有过客户因为我的标准差增加而给我打电话或更糟糕地解雇我。我知道论点是更高的标准差会导致更高的回撤，但正如我稍后在帖子中展示的，情况似乎并非如此。

![](http://www.advisorbenchmarking.com/)

客户会打电话给我或者解雇我，因为他们亏了钱，所以如果我能尽量减少回撤的频率、幅度和持续时间，那么我就能帮助/引导客户减轻担忧，这也是他们支付我的主要原因之一。此外，虽然我认为专注于减少回撤可以显著提高实现他们长期回报目标的机会([回撤控制也能决定最终财富](http://timelyportfolio.blogspot.com/2011/07/drawdown-control-can-also-determine.html)和[信心、最终股权以及我能作为资金经理做什么](http://timelyportfolio.blogspot.com/2011/06/confidence-ending-equity-and-what-i-can.html "信心、最终股权以及我能作为资金经理做什么"))，这甚至更可能是客户支付我的原因。

如果回撤也能决定一个目标系统的成功与否，那该有多好？为了开始测试，我原想利用[大卫·圣约翰](http://www.math.uic.edu/mslc/?sid=profile&unid=dstjoh2)在 ttrTests 上的优秀工作([ttrTests 第四版和最终版测试](http://timelyportfolio.blogspot.com/2011/10/ttrtests-4th-and-final-test.html))，从月度标普 500 数据中获取 100,000 个引导样本，来研究回撤、标准差、偏度以及买入持有与[Mebane Faber 10 个月移动平均系统](http://www.mebanefaber.com)的复合回报。由于我如此有偏见，我会让你来判断回撤对结果的重要性。

这里是我对自己信念的信心所在：更高的标准差并不一定导致更差的回撤。然而，有趣的是，更高的标准差与系统表现不佳（或者说超常表现）之间的相关性不亚于回撤（右下角）。

以下是来自 GIST 的[R 代码](https://gist.github.com/1418765)：
