```yml

分类：未分类

日期：2024-05-12 18:56:45

→

# 量化交易：开源遗传算法软件（嘉宾文章）

> 来源：[`epchan.blogspot.com/2015/10/an-open-source-genetic-algorithm.html#0001-01-01`](http://epchan.blogspot.com/2015/10/an-open-source-genetic-algorithm.html#0001-01-01)

作者：**Lukasz Wojtow**

机械交易员从未停止寻找下一个市场优势。不仅为了获得更好的结果，而且还因为拥有多个系统。通过同时交易多个非相关的系统可以实现最佳的交易成果。不幸的是，大多数交易员使用类似的市场无效性：一些交易员专门从事趋势跟踪，一些从事均值回归等等。那是因为学习利用一种优势已经足够困难，掌握所有这些——不可能的。拥有能够创建许多不相关系统的软件将是有益的。

最近我发布了 Genotick——一个开源软件，可以创建和管理一组交易系统。Genotick 的核心是一个启示：如果仅用几条汇编指令就能创建任何软件，那么也应该有可能用同样简单的一组指令创建任何交易系统。这些简单且单独无意义的指令当组合在一起时会变得极其强大。顺序正确的正确指令可以创建任何类型的机械系统：趋势跟踪、均值回归，甚至基于基本数据。

驱动 Genotick 强大功能的引擎是一种遗传算法。目前的实现相当基础，但有一些额外的怪癖。例如，如果任何一个系统表现得真的很糟糕——它仍然留在群体中，但它的预测被反转了。另一个技巧是用来帮助识别有偏见的交易系统：如果一个系统在镜像数据上没有产生镜像预测，那么它可以被移除。所以例如，GBP/USD 上的头寸必须与 USD/GBP 上的头寸相反。Genotick 还支持可选的精英主义（其中最好的系统总是留在群体中，而其他系统则因年龄大而被淘汰），对新系统的保护（避免移除尚未有机会证明自己的系统）以及从父母继承初始系统权重。这些选项给用户留下了大量的实验空间。

当 Genotick 第一次运行时 - 没有系统。它们在开始时使用随机选择的指令创建。然后，遗传算法接管：每个系统都用于检查其在历史数据上的预测。预测正确的系统在未来的预测中增加权重，预测错误的系统失去权重。随着时间的推移，每天人口的增长。差的系统被移除，好的系统繁殖。每天的预测是通过添加当时可用的所有系统的预测来计算的。Genotick 不会多次迭代相同的历史数据 - 训练过程看起来就像是在现实生活中执行一样：一天一天地进行。实际上，没有单独的“训练”阶段，程序随着每一天的推移而稍微学习。

有趣的是，Genotick 不会检查创建系统的理由。由于每个系统都是随机指令创建的，因此可能（实际上非常可能）某些系统使用荒谬的逻辑。例如，一个系统可能会在 42 天前成交量 positive 时给出“买入”信号。另一个系统可能希望每次昨天的最高价的第三位数字与今天的开盘价的第二个数字相同时做空。当然，这样的系统在现实世界中永远不可能生存，而且在 Genotick 的群体中也生存不了多久。因为每个系统的初始权重为零，它们永远不会获得任何 significant 权重，因此不会破坏程序给出的累积预测。一开始就允许这样的系统似乎有点愚蠢，但这使得 Genotick 能够测试不受交易者信仰、误导性观点和个人局限性影响的算法。可悲的事实是，市场不在乎你使用什么系统，以及你投入了多少汗水和泪水。市场会做它想做的事情——没有问题，不带走任何俘虏。市场甚至不在乎你是否使用任何形式的智力，无论是人工的还是其他的。因此，每个交易系统的唯一理由应该非常简单：“它有效吗？”。没有更多，没有更少。这是 Genotick 衡量系统的唯一指标。

每个程序的运行都会略有不同。下面的股票图表显示了一种可能的绩效。显示的年份是从 2007 年到 2015 年，实际的训练始于 2000 年。2007 年并没有什么特别的，记住——Genotick 随着运行而学习。然而，我觉得它在金融危机期间的性能很重要。交易的市场包括：

美元/瑞士法郎，美元/日元，10 年美国国债收益率，SPX，欧元/美元，英镑/美元和黄金。

（在某些情况下，我使用市场指数如 SPX 测试系统，而不是跟踪指数的仪器如 SPY，但差异应该很小。）所有市场都被镜像，以允许移除有偏见的系统。一些关键数字：

复合年化增长率：9.88%

最大回撤：-21.6%

最长回撤：287 个交易日

盈利交易日：53.3 %

卡马尔比率：0.644

夏普比率：1.06

年均收益平均值：24.1%

亏损年份：2013 年（-12%）

（点击下面的累积回报百分比图表以放大。）

| ![累积回报](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhFGAHlup3ESxhuboRWWsCSC-H-HfuIQHR-c50b3KSHlXivn1PJ_1e6ZFuXLV7CZmqXfE2LoWeLgSLoxgn38gW-76nyZu_gYp1s1QGB9ppUqaGzpmstg69wQSqUwBB1JbSbrmdWyg/s1600/equity.png) |
| --- |
| 自 2007 年以来的累积回报（%） |

这些数字仅代表了软件所提供的“方向性优势”。没有止损，没有杠杆和没有仓位大小，这可能会极大地改善真实生活的结果。假设在每天结束时，仓位都会重新平衡，使每个工具都以相等的美元价值开始。（即这是一个恒定再平衡的投资组合。）

人工智能是一个热门话题。自动驾驶汽车比普通人类驾驶得更好，国际象棋算法能打败普通玩家都是事实。不同的是，用 AI 进行交易是完全合法的，对手可能永远不知道。与国际象棋和驾驶不同，金融市场中有大量的随机性，而且可能需要更长的时间才能注意到当 AI 开始赢。尽管最佳对冲基金仍然可以由人类管理，但如果任何交易方法确实更优越，AI 也会发现。

目前 Genotick 更像是一个概念验证，而不是生产准备。

它的可用性非常有限，它不会原谅错误，最好在用于真实交易之前先咨询。你需要 Java 7 来运行它。它在 Linux 和 Windows 10 上都经过测试。包含示例历史数据。任何问题或评论都受欢迎。

===

**我的即将举行的工作坊**

动量策略在近期市场动荡中表现出色，因为它们看多波动性。本课程将涵盖各种资产类别和不同交易周期的动量策略。

====

关注我：@chanep
