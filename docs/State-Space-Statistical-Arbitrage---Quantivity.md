<!--yml

类别：未分类

日期：2024-05-18 13:53:35

-->

# 状态空间统计套利 | Quantivity

> 来源：[`quantivity.wordpress.com/2010/02/15/state-space-statistical-arbitrage/#0001-01-01`](https://quantivity.wordpress.com/2010/02/15/state-space-statistical-arbitrage/#0001-01-01)

在[Trading the Unobservable](https://quantivity.wordpress.com/2010/02/15/trading-the-unobservable/)的机器学习焦点基础上，Triantafyllopoulos 和 Montana 最近发表了一篇关于统计套利的状态空间模型，题为[Dynamic Modeling of Mean-reverting Spreads for Statistical Arbitrage](http://arxiv.org/PS_cache/arxiv/pdf/0808/0808.1710v3.pdf)。本文是基于 2005 年 Elliott *等人* 在[JQF](http://www.tandf.co.uk/journals/rquf)上发表的文章《Pairs Trading》的延伸。

本文的贡献，摘要如下：

> 基于先前的工作，我们采用状态空间框架来建模传播过程，并沿三个不同方向扩展这一方法论。首先，我们在模型参数中引入时间依赖性，这允许快速适应数据生成过程的变化。其次，我们提供了一种可以实时持续运行的在线估计算法。由于计算速度快，该算法特别适用于基于高频数据构建激进交易策略，并可用作均值回归的监控装置。最后，我们的框架自然地提供了所有估计参数的信息不确定性度量。

对于那些使用 PCA 或协整技术进行统计套利交易的人（或熟悉 Avellaneda 和 Lee 在 [Statistical Arbitrage in the U.S. Equities Market](http://www.math.nyu.edu/faculty/avellane/AvellanedaLeeStatArb071108.pdf) 中的工作），本文提供了有趣的理论比较。
