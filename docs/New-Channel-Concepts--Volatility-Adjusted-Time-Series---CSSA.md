<!--yml

分类：未分类

日期：2024-05-12 17:48:39

-->

# 新的通道概念：波动调整时间序列 | CSSA

> 来源：[`cssanalytics.wordpress.com/2015/02/12/new-channel-concepts-volatility-adjusted-time-series/#0001-01-01`](https://cssanalytics.wordpress.com/2015/02/12/new-channel-concepts-volatility-adjusted-time-series/#0001-01-01)

![vol33](https://cssanalytics.files.wordpress.com/2015/02/vol33.jpg)

在过去的几篇文章中，我介绍了一些不同的通道策略方法，包括[百分位通道](https://cssanalytics.wordpress.com/2015/01/21/percentile-channels-a-new-twist-on-a-trend-following-favorite/ "百分位通道：趋势跟踪的新变化")。一个简单的方法，可以潜在地改进（或至少采用不同的方法）唐奇安通道策略，就是使用不同的价格输入来生成交易信号。如在[误差调整动量再现](https://cssanalytics.wordpress.com/2015/02/02/error-adjusted-momentum-redux/ "误差调整动量再现")中所述，使用任何类型的风险调整都有助于通过减少一些噪音来提高性能。当使用回报时，这很容易应用，但是当我们将此概念应用于基于价格的策略时该怎么办呢？实际上很简单：使用一个固定的目标百分比-比如 1%-，你将自始至终的所有回报乘以目标除以某个滞后标准差。然后你创建一个这些回报的指数，这将成为新的价格系列（要小心避免任何前瞻性偏差）。这个波动调整指数就是生成您的通道策略信号的东西，而不是传统的价格历史。当然，在回测中，你获得的是实际价格历史上的回报，而不是波动调整指数上的回报。作为最后澄清的一点，你并不是根据波动性来改变你的头寸大小，而是只是改变输入价格。

所以，让我们比较使用传统的 120 日唐奇安通道策略，即在标普 500 指数创下 120 日新高时买入，并在 120 日新低时卖出并持有现金（SHY），与使用波动调整时间序列生成信号的相同策略。回顾期是 20 日标准差，将每日回报调整为创建指数（带有 0.75%的波动目标-注意目标选择不会改变性能，只会改变指数的比例）。对于这个测试，我们使用了来自 Yahoo 的 SPY 数据，以及从 Morningstar 延伸的 SHY 数据。请注意，红线不是策略的股权曲线，而是使用 SPY 创建的波动调整指数。使用该指数进行信号的策略表现也用红色突出显示：

![SPY VOLLY](https://cssanalytics.files.wordpress.com/2015/02/spy-volly.png)

在这种情况下，使用波动率调整指数相对于实际 SPY 价格，可以提高性能。以下是仅使用 DBC 和 ETF 数据（因为 DBC 的扩展选择可能会导致性能出现显著的变异性）的相同策略：

![带有波动率的 DBC](https://cssanalytics.files.wordpress.com/2015/02/dbc-with-volly.png)

该策略显示出一些潜力，并在某些时候产生与传统策略不同的信号。或许使用不同的风险度量，如加速度，或者使用其他过滤技术可能会带来更大的希望。这个概念可以与移动平均线或其他基于价格的信号一起应用。这是勤奋的研究者可以尝试的另一个概念。或许将分形应用于生成图表可能是另一种有用的探索途径。
