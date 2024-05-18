<!--yml
category: 未分类
date: 2024-05-18 13:53:35
-->

# State Space Statistical Arbitrage | Quantivity

> 来源：[https://quantivity.wordpress.com/2010/02/15/state-space-statistical-arbitrage/#0001-01-01](https://quantivity.wordpress.com/2010/02/15/state-space-statistical-arbitrage/#0001-01-01)

Building upon the ML focus from [Trading the Unobservable](https://quantivity.wordpress.com/2010/02/15/trading-the-unobservable/), Triantafyllopoulos and Montana recently published a state space model for statarb spreads entitled [Dynamic Modeling of Mean-reverting Spreads for Statistical Arbitrage](http://arxiv.org/PS_cache/arxiv/pdf/0808/0808.1710v3.pdf). This article builds upon the 2005 Elliott *et al.* article Pairs Trading in [JQF](http://www.tandf.co.uk/journals/rquf).

Contribution of this paper, per the abstract:

> Building on previous work, we embrace the state-space framework for modeling spread processes and extend this methodology along three different directions. First, we introduce timedependency in the model parameters, which allows for quick adaptation to changes in the data generating process. Second, we provide an on-line estimation algorithm that can be constantly run in real-time. Being computationally fast, the algorithm is particularly suitable for building aggressive trading strategies based on high-frequency data and may be used as a monitoring device for mean-reversion. Finally, our framework naturally provides informative uncertainty measures of all the estimated parameters.

For those who have traded statarb using PCA or cointegration techniques (or are familiar with [Statistical Arbitrage in the U.S. Equities Market](http://www.math.nyu.edu/faculty/avellane/AvellanedaLeeStatArb071108.pdf) by Avellaneda and Lee), this article provides interesting theoretical comparison.