<!--yml

类别：未分类

日期：2024 年 5 月 12 日 23:15:53

-->

# Falken 博客：残余方差怎么样？

> 来源：[`falkenblog.blogspot.com/2008/06/what-about-residual-variance.html#0001-01-01`](http://falkenblog.blogspot.com/2008/06/what-about-residual-variance.html#0001-01-01)

当我在进行我的

[论文](http://www.efalken.com/papers/aVolatilityPapers/EF%20Dissertation.pdf)

关于方差和股票回报，我记得特异波动性和系统波动性间可能存在巨大的差别。系统波动性基本上是 beta 的平方，与 beta 计算周期的市场波动性相乘。而残差或特异波动性，则是总波动性与系统波动性之间的差异。

这显然在测试方差上有很大的差别，因为我们都知道 beta 的问题。由于各种原因，条件波动问题，使用正确的指数（标普 500，市值加权 CRSP 指数，等权重指数等），它的测量可能带有误差。因此，如果你发现了总体方差或系统方差与回报之间的相关性，祝你好运。beta 是如此受到影响，如此值得怀疑，以至于你无法对它做出任何评论。因此，最近 Ang、Hodrick、Xing 和 Zhang 的论文（

[美国](http://www2.gsb.columbia.edu/faculty/aang/papers/vol.pdf)

和

[国际](http://www2.gsb.columbia.edu/faculty/aang/papers/ivol.pdf)

），关于波动性和回报的是“特异波动性”和横截面回报。

但我记得我读了 Bruce Lehman 写的一篇有趣的文章，

[重新审视残余风险](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=344750)

。他指出，特异波动性应该捕捉到被错误估计的因子载荷，而被错误估计的因子载荷应该能够解释 APT 等因子模型的糟糕表现。例如，

[Stephen Ross 和 Richard Roll](http://www.afajof.org/journal/jstabstract.asp?ref=11410)

（1994 年）指出，市场组合的无效估计可能与回报不相关，但残余应该仍然与回报呈正相关。也就是说，如果某个因素估计错误，那么 beta 的测量就不完美，因为风险代理的不完美。但在这种方程中的残差方差应该与回报呈正相关。

最近，我汇总了大量有关 beta、总体波动性和残差波动性的数据。无论你怎么看，你得到的结果都差不多。它们在横截面上都与回报呈负相关。就预期回报而言，这无所谓。嗯。我在想

[为何](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=976652)

? 研究生学校从来没有告诉你，实际上，风险非常非常微妙。
