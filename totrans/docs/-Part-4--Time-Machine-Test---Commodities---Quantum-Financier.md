<!--yml
category: 未分类
date: 2024-05-18 14:03:40
-->

# (Part 4) Time Machine Test – Commodities – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2010/05/13/151/#0001-01-01](https://quantumfinancier.wordpress.com/2010/05/13/151/#0001-01-01)

Results on a commodities basket.

WTI Crude
[![](img/c7314e04a3403fc4642717747efa3f54.png "Time Machine Test Wilcox - WTI Crude")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-wilcox-wti-crude1.png)

Natural Gas
[![](img/80dd234384d086a0bb685aeded7f0357.png "Time Machine Test Wilcox - Natural Gas")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-wilcox-natural-gas1.png)

Gold
[![](img/80c21653f25ac5f92a4764e2c3ade499.png "Time Machine Test Wilcox - Gold")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-wilcox-gold1.png)

Silver
[![](img/6b07c65a052a86857f462ab392c8cf4b.png "Time Machine Test Wilcox - Silver")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-wilcox-silver1.png)

Results
[![](img/4e45cbd41c62979fcbd786301121dce6.png "Time Machine Test Wilcox - ResultsComm")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-wilcox-resultscomm1.png)

As you can see, the algorithm adapts to different classes of commodities and outperforms most of the buy and hold returns. But I want to emphasis that this concept alone is not something I would trade as is (not robust enough). The results are in no way good enough to rely on out-of-sample.

I found that it is much harder for the algorithm to find strategies significant enough to trade on for long periods on these assets. For equities, there is on average 7 different active strategies (i.e. the level of significance is high enough) at the same time. The number is much less with commodities and currencies, the lack of diversification between strategies certainly hurts performance when compared to equity indices. It also add on more exposure to a given strategy adding a lot of volatility to the returns as showed by the numbers above.

QF