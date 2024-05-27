<!--yml

category: 未分类

date: 2024-05-12 20:54:00

-->

# Falkenblog: 高频交易论文

> 来源：[`falkenblog.blogspot.com/2011/05/high-frequency-trading-paper.html#0001-01-01`](http://falkenblog.blogspot.com/2011/05/high-frequency-trading-paper.html#0001-01-01)

我涉足于高频交易，所以我不再多作评论；当然

不是

向人们透漏你在某个主题上的所有想法是最优策略。但是，有关 Easley，de Prado 和 O'Hara 新的波动率指标的文章相当受欢迎，

[在高频交易世界中的流动性毒性和波动性](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1695596)

因此这并非是内部消息。噢哈拉（O'Hara）似乎已经在这个领域写了几十年的文章，她在这个领域是一个非常专业的作者。事实上，de Prado 与图德尔对冲基金有牵连，而且他们允许他公开发表这个，这凸显了这个信息本身并不具有价值。但是，很多有用的工具并不明显地转化为金钱，所以这并不是一个很大的冲击。

他们的交易概率分析(Volume-Synchronized Probability of Informed Trading，或者 VPIN)是这样的：

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjyjVVM7GkTuwEpFmXU7T1oGNEQIi-QwuE7UvnTD23KbJSIMo2VQ4GepCC-MpUr61KHra2TaJpTuhXZsyIVw_X4FsFKP41Ji8R_cdboDvQVOnW3hyphenhyphenMFebANTUPINBttYwNy-uVt_g/s1600/vpin.jpg)

在 gif 图中很难看到，但编号里 Vb 是买入量，假设是当一个交易价格大于或等于上一笔交易价格时，Vs，或者卖出量，反之。因此，在过去，比如交易了 10000 股，买入量与卖出量的不平衡就越大，那么这个指标就越大。这些都出现在任何一个容器中过去交易的价格内，n 代表样本的容器数。因此，评估是在交易空间内进行的，而不是时间空间内，作者认为这样更稳定和更具有意义。

下图显示了这个指标如何预测未来的交易波动性。请注意，随着 VPIN 的对数上升，价格波动幅度会增加。这并非完美的关系，但没有什么重要的。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgzWon0FQjajY1w08juHy8fk8XcBig9-vkX4DGPmIt5GUtjqFtcm1lqjd12oAoHOUO91go3s_0lQ1hrb4FAY-Dq8sln9LxDb3DsjI1_LBRS9SWujos9bNJSccKMYbXbRKdQD72Mgw/s1600/vpinvol.jpg)

在快速变动的市场中，人们需要的不仅仅是简单的历史日收盘价的移动平均值。这种方法更好，将'成交量时间'与'历史时间'的概念延伸开来是一个有趣的方向。而人们也可以直接观察买卖价差，或者观察 VIX 期货，或者它的交易所交易基金 VXX，以及这些指标的组合，来评估盘中波动性。另外，人们可以更好地估计'买入量'，使用的是交易价格相对于当时的买卖价差，而不是价格是否有弱涨，尽管这会涉及将交易信息与报价信息同步，对于学术界来说这些数据往往难以获得（此外，报价信息往往是交易信息的十倍）。
