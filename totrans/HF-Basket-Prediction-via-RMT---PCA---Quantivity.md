<!--yml
category: 未分类
date: 2024-05-18 13:53:17
-->

# HF Basket Prediction via RMT / PCA | Quantivity

> 来源：[https://quantivity.wordpress.com/2010/08/22/high-frequency-prediction-via-rmt-pca/#0001-01-01](https://quantivity.wordpress.com/2010/08/22/high-frequency-prediction-via-rmt-pca/#0001-01-01)

What if *robust* principal components could be identified for arbitrary baskets *in real-time* and used for HF *intra-day* prediction? Such would be an essence of high-frequency [market regimes](https://quantivity.wordpress.com/2009/12/31/market-regime-trading-redux/).

[Tanaka-Yamawaki](http://irene.ike.tottori-u.ac.jp/mieko/profile_e.html) posits the emerging existence of such a methodology in an [abstract](http://www.phys.sinica.edu.tw/~socioecono/econophysics2010/pdf/TanakaYamawakiAbstract.pdf) for upcoming [KES2010](http://kes2010.kesinternational.org/) and [Econophysics Colloquium 2010](http://www.phys.sinica.edu.tw/~socioecono/econophysics2010/). This work builds upon Plerou *et al.*, who pioneered applying [random matrix theory](http://en.wikipedia.org/wiki/Random_matrix) (RMT, aka stochastic eigenanalysis) to analysis of cross-correlations of equity price changes in [Random Matrix Approach to Cross Correlation in Financial Data](http://arxiv.org/abs/cond-mat/0108023).

While the concept of applying real-time PCA is hardly new, what may be new is: use of RMT for rigorously separating correlation signal from noise, doing so in real-time, and focus on intra-day prediction.

More specifically, Tanaka-Yamawaki introduces:

> Some stocks exhibit strong correlation to other stocks…However, the networks of such correlation are unstable and the patterns are only temporal. In such a condition, a detailed description of the network may not be very useful, since the situation quickly changes and the past knowledge is no longer valid under the new environment. If, however, we have a **methodology to extract, in a very short time, major components that characterize the motion of the market, it should give us a powerful tool to describe temporal characteristics of the market** and help us to set up a time varying model to predict the future move of such market

This analysis seems potentially fruitful along two dimensions:

*   HF dynamics: Plerou focused on lower-frequency (30-minute and daily) returns, thus missing out on high-frequency dynamics
*   HFT: interesting to identify which (if any) types of high-frequency trading effects are visible, as some are unlikely to be visible (*e.g.* single instrument front-running) while others may be visible (*e.g.* index arb)

Will be interesting to read the proceedings, when they are published.