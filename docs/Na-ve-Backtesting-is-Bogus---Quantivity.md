（以下内容为注释，不翻译）

类别：未分类

日期：2024-05-18 13:55:55

（以下内容为注释，不翻译）

# 简单的回测是伪的 | Quantivity

> 来源：[`quantivity.wordpress.com/2009/08/16/naive-backtesting-is-bogus/#0001-01-01`](https://quantivity.wordpress.com/2009/08/16/naive-backtesting-is-bogus/#0001-01-01)

量化交易最常被引用的[传统智慧](http://en.wikipedia.org/wiki/Conventional_wisdom)是回测，通常总结为：

> 明智的交易者尽可能多地进行[回测](http://en.wikipedia.org/wiki/Backtesting)后再开始用真实资金交易系统。

不幸的是，这种智慧是伪的。更准确地说，当按照标准的回测公式实践时*这种智慧是伪的*：

1.  指标：选择指标（无论是基本面、技术面还是统计面）

1.  数据：选择某种工具的长期数据面板（通常是尽可能多的数据）

1.  回测：给定指标，在数据面板中优化入场和出场构建策略

1.  盈利！

是的，毫无疑问有些交易者用这个公式找到了短期成功。这实际上是由于[无限猴子定理](http://en.wikipedia.org/wiki/Infinite_monkey_theorem)：足够多的交易者在强大的计算机上进行足够多的[数据窥探](http://en.wikipedia.org/wiki/Data-snooping_bias)最终会导致一小部分人发现由于纯粹的随机性而看起来成功的策略。

考虑一个汽车比喻，以帮助说明这个公式的谬误：预测未来[油粘度](http://en.wikipedia.org/wiki/Viscosity)，给定在先前一段时间内随机时间点的油粘度测量值。这些测量值具有以下统计属性：

+   随机分散：值随机出现，大致遵循[布朗运动](http://en.wikipedia.org/wiki/Brownian_motion)

+   两个主要的群集：值大致围绕两个主要[群集](http://en.wikipedia.org/wiki/Cluster_analysis)

+   随机异常值：两个主要群集之间的随机异常值存在，大部分位于连接两个群集的平面上

这些测量值非常粗略地遵循交易员在牛市/熊市周期（上述比喻中的群集）观察到的低频证券价格（上述比喻中的油）。鉴于这一点，回到预测：给定过去，未来油粘度的值会是什么？多年努力可能投入到分析这一问题，运用各种应用数学方法获得了有限的预测性。读者被鼓励思考这个挑战，假设他们给出的数据不超过上述内容。

量化交易的很大一部分类似于这个油粘度问题：盲目地回测众多观测测量值，严格地使用不同的数学方法优化参数。

现在，考虑一个额外的发现：被测量的油包含在一个引擎中，它在一段时间内随机地在“开启”和“关闭”之间变化。有了这个知识（知道运行的引擎是热的），量化分析师会很快想起温度和粘度之间的关系。不久之后，有人会将[萨瑟兰公式](http://en.wikipedia.org/wiki/Viscosity#Effect_of_temperature_on_the_viscosity_of_a_gas)与[聚类分析](http://en.wikipedia.org/wiki/Cluster_analysis)结合起来，并确定一种有效的预测方法。

如果交易者在 2007 年至 2009 年（或 1998 年至 2002 年）期间学到了任何东西，那应该就是经济学和金融的基本原理并不稳定：*几乎所有常用统计衡量指标在几乎所有资产类别中都表现出了不一致的行为*（平均值、方差、波动性、协方差、相关性、协整性、主成分、偏度、峰度、*等等*）。初级经济学告诉我们，这些不稳定的根本原因有很多，从[商业周期](http://en.wikipedia.org/wiki/Business_cycle)到[货币政策](http://en.wikipedia.org/wiki/Monetary_policy)。

然而，尽管有这些直接的观察，许多交易者仍然愉快地按照自己的方式继续前进，继续忠诚地相信回测的智慧。根据上述类比，交易者会从完善他们的量化方法以适应系统偏差中受益——而不是盲目地进行长期回测，不关心诸如市场体制等[外部性](http://en.wikipedia.org/wiki/Externality)。

真正的挑战是* somehow refining the methodology of quantitative trading in response to this knowledge*。后续文章将努力应对这一挑战，希望读者能贡献他们的专业知识。
