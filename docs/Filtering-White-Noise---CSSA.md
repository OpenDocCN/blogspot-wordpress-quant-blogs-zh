<!--yml

类别：未分类

日期：2024-05-12 18:00:10

-->

# 过滤白噪声 | CSSA

> 来源：[`cssanalytics.wordpress.com/2013/04/23/filtering-white-noise/#0001-01-01`](https://cssanalytics.wordpress.com/2013/04/23/filtering-white-noise/#0001-01-01)

![](img/078bb421694066e19ebf093a38eac995.png)

大多数资产回报过程可以被描述为包含一个主要趋势，以及围绕该趋势的均值回归，以及一定量的随机噪声。经济计量学家使用[Hurst 指数](http://en.wikipedia.org/wiki/Hurst_exponent)将这些元素分类为：1)黑噪声（趋势/正自相关性- Hurst>.5）2)粉红噪声（均值回归/负自相关性- Hurst<.5）或 3）[白噪声](http://en.wikipedia.org/wiki/White_noise)（无趋势/均值回归，低/不显著的自相关性- Hurst=.5）。直观地，交易者希望利用趋势或均值回归行为中的任一行为- 通常在不同的时间框架内，因为它们是同一统一过程的一部分（趋势往往发生在较长的时间框架内，而围绕该趋势的均值回归发生在较短的时间框架内）。这两种风格的关键障碍是消除或最小化对用于衡量趋势或均值回归行为的指标的白噪声的影响。未能这样做会导致由于虚假/随机信号而导致的糟糕交易结果。

考虑同一时间序列的两个图表（来自[Jonathan Kinlay 的优秀博客](http://jonathankinlay.com/)），一个是黑噪声过程，另一个包含白噪声过程：

![黑噪声分形随机漫步](https://cssanalytics.files.wordpress.com/2013/04/black-noise-fractal-random-walk.png)

![白噪声随机漫步](https://cssanalytics.files.wordpress.com/2013/04/white-noise-random-walk.png)

在第一个图表中- 使用黑噪声过程- 很容易看出使用简单移动平均线来交易基础资产可能是多么有利可图- 几乎没有什么噪声不是自我强化的（趋势）。在第二个图表中- 使用白噪声过程- 您可以看到与真实金融时间序列的相似之处。看起来有相当多的随机噪声，例如使用移动平均线进行交易会更加困难。下面的图表显示了一个粉红噪声过程，并且对于那些交易对的人来说是熟悉的，这些交易对是两个资产价格的对数，这些资产是协整的（即类似于一个部门 ETF 与不同 ETF 提供商的相同部门）。

![粉红噪声](https://cssanalytics.files.wordpress.com/2013/04/pink-noise.png)

请注意，这个过程似乎具有稳定的平均值和可预测的负自相关性。使用基于移动平均线的趋势策略来交易这个系列是不可能的。然而，这将是使用运行进行交易（例如，在下跌日买入，在上涨日做空）的理想数据集。实际上，时间序列数据包含了所有三种类型的噪声元素，因此我们想做的是过滤掉白噪声，因为白噪声不太可预测，会掩盖本来可以预测的资产行为。

一位同事 George Yang 最近写的一篇[最新论文](http://ssrn.com/abstract=2260609)揭示了如何筛选随机/白噪声因素，并展示了对交易系统盈利能力的实际影响。该论文最近在著名的[Wagner Award](http://www.naaim.org/resources/wagner-award/)比赛中获得了奖项，该比赛由[NAAIM](http://www.naaim.org/://)举办。杨先生表明，可以使用滚动或历史标准差阈值来滤除“不重要”的数据，并将指标扩展为仅使用“重要”的数据。例如，如果要在 S&P500 上使用 200 天移动平均线，您可能会规定市场波动在 0.25%和-0.25%之间的情况是太小，无法被视为定义趋势的重要因素。也就是说，小幅度的上升或下降日（或一系列小日）可能导致一笔交易，但这并不意味着潜在趋势的真正变化。可以将此转化为滚动标准差单位的一部分来计算真正的 200 天移动平均值。在第一种情况中，要计算出真正的 200 天移动平均值，必须从数据集中排除所有不重要的日，并向后追溯，直到有 200 天的重要数据可用于计算移动平均值。论文中的结果表明，这种筛选方式可以有效增加信号与噪音的比率，并在各种参数范围内改善交易结果。该论文还表明，相同的技术对改善利用运行的短期均值回归系统也有效。这突显了可以将白噪声从数据中过滤出来的应用潜力。

有多种扩展来改进这个概念，其中许多超出了此帖子的范围。然而，一个表面上显而易见的方法是过滤掉不重要的交易日，同时要求交易量也不重要--很可能低于平均水平的交易量表明市场对当前价格没有明确的共识。另一方面，伴随着非常大的交易量的看似小小的市场波动可能是一个警示信号。另一种方法可以(根据乔治的建议)查看当天的高低幅度与过去的关系(比如 DV2)。很可能一个较窄的日幅意味着不重要的波动，而一个较大的幅度更具信息量。人们可以想象使用多个过滤器来增强识别真正重要的交易日与无关紧要的交易日的能力。这将进一步显著改善交易信号的表现或预测能力。
