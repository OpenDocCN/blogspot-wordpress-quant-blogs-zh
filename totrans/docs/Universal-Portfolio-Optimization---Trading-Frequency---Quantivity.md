<!--yml
category: 未分类
date: 2024-05-18 13:54:54
-->

# Universal Portfolio Optimization & Trading Frequency | Quantivity

> 来源：[https://quantivity.wordpress.com/2010/01/02/universal-portfolio-optimization/#0001-01-01](https://quantivity.wordpress.com/2010/01/02/universal-portfolio-optimization/#0001-01-01)

Readers with background in portfolio selection and optimization may be interested in a recent working paper by Hazan and Kale, presented at [NIPS 2009](http://books.nips.cc/nips22.html): On Stochastic and Worst-case Models for Investing.

This paper builds upon Agarwal *et al.*, Algorithms for Portfolio Management Based on the Newton Method (2006); and Cover, [Universal Portfolios](http://www.stanford.edu/~cover/papers/paper93.pdf) (1991). Notable is this research theme is beginning to actually intersect with reality, suggesting the potential for practical trading applicability.

Specifically, Lemma 11 makes an interesting claim relating variance of the minimum variance CRP with trading frequency (p. 8); prose summary of this lemma is:

> Thus, increasing the trading frequency decreases the variance of the minimum variance CRP, which implies that it gets less risky to trade more frequently; in other words, the more frequently we trade, the more likely the payoff will be close to the expected value. On the other hand, as we show in Theorem 10, the regret does not change even if we trade more often; thus, one expects to see improving performance of our algorithm as the trading frequency increases.

Interesting that portfolio optimization papers are now beginning to comment formally on trading frequency optimality, albeit in characteristically stylistic ways.