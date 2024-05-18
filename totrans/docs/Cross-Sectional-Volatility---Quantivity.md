<!--yml
category: 未分类
date: 2024-05-18 13:52:45
-->

# Cross Sectional Volatility | Quantivity

> 来源：[https://quantivity.wordpress.com/2011/03/02/cross-sectional-volatility/#0001-01-01](https://quantivity.wordpress.com/2011/03/02/cross-sectional-volatility/#0001-01-01)

[Delay Embedding as Regime Signal](https://quantivity.wordpress.com/2011/02/24/delay-embedding-as-regime-signal/) prompted enough questions to warrant further commentary on the *principal component space* ![D](img/fd6081407ca943a923c743cb5596009a.png) and *cross-sectional volatility* ![\sigma_D ](img/caace9246a12cff17c95ed38373b7ec8.png) models, from which the regime signal ![E_H ](img/ed892cc9f94ea8c49725a477cca991f6.png) is derived. Understanding both are worthwhile for two reasons:

*   Lineage: this model is *stylistically* representative of the statarb tradition, spanning from [Computational Methodology for Modeling the Dynamics of Statistical Arbitrage](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.99.6514) (Burgess, 1999) to [Statistical Arbitrage in the US Equities Market](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1153505) (Avellaneda and Lee, 2008); on the practical side, both Burgess and Neil Yelsey (acknowledged by Infantino and Itzhaki) are reputed to have run arbitrage desks
*   Exemplary: this illustrates how to build models which are *transformations of returns* (commonly via [dimensional reduction](http://en.wikipedia.org/wiki/Dimension_reduction)), rather than returns themselves—as Paul Grimoldi commented; this also speaks to Jeff’s question last year regarding the contrast of classic technical analysis with quantitative methods: visual pattern analysis of returns versus statistical analysis / ML on transformed returns

Intuition of this model is compelling, albeit obfuscated fairly heavily by its rough mathematical presentation: *mean-reverting convergence can be predicted via a dimensionally-reduced (principal components) [space](http://en.wikipedia.org/wiki/Vector_space) of returns from an equity portfolio*. The following seeks to explain this intuition, including use of more standard mathematical language than found in § 2.4 and § 3.1\.

First step is to choose a dimensional reduction to *denoise the returns*, providing a transformed basis for predicting returns. Doing so is justified by the assumption that “main risk factors should drive the stock’s returns in a systematic way, and the residuals as the noise to get rid” (p. 30), thus echoing [CAPM](http://en.wikipedia.org/wiki/CAPM) in that return is justified by risk (yet another [wonder of residuals](https://quantivity.wordpress.com/2009/08/02/wonder-of-residuals/)).

The trick is identifying anonymous equity *risk factors*, and using them to guide denoising and [feature extraction](http://en.wikipedia.org/wiki/Feature_extraction). [Principal component analysis](http://en.wikipedia.org/wiki/Principal_component_analysis) (PCA) is a natural choice, as principal components are chosen to maximize variance and thus naturally capture “risk” in the realized sense. PCA is further compelling as the corresponding eigenspace defines a *principal component space* which naturally serves as a [feature vector](http://en.wikipedia.org/wiki/Feature_vector) for statistic / ML analysis.

Denoising occurs by choosing a small number of the dominant PCA eigenvectors and composing them into the matrix ![D](img/fd6081407ca943a923c743cb5596009a.png). The eigenvectors which are omitted, those which only explain a small percent of variance, are thus considered “noise”. Presumably assumed justification is again based on CAPM: any eigenvector which does not explain systematic variance (*i.e.* risk) cannot explain systematic return. The number of ![k](img/7881e4ad2e7a375a9b4dd9dea1f6a3ae.png) is remarked to be 4 – 5, collectively explaining over 80% of variance (footnote 19).

Second step is to define *prediction via the dimensionally-reduced principal component space*:

     ![\hat{S} = S + M = \hat{D_t} * B + M = \sum\limits_{i = 0}^{H - 1} D_{t - i} * B + \frac{1}{T} \sum \limits_{t=1}^T X_t^n ](img/1bb0d83036811e61358ede8b787f5dd6.png)

where ![B ](img/24fe175b0a6620d2232eb458ad204964.png) are estimates from a long-horizon regression and ![M](img/eb44ec3c0dcc9f29a8750db07e9e5890.png) are the return means. Recall that PCA assumes *de-meaned* returns (see [Karhunen–Loève](http://en.wikipedia.org/wiki/Karhunen%E2%80%93Lo%C3%A8ve_theorem) for explanation why), thus the mean must be added back to generate the prediction.

Use of a *long-horizon regression* to generate ![B](img/ab996e403e502a251f67bad9d08029aa.png) is particularly interesting, as one is left to speculate given lack of stated justification (and authors’ misspelling). Historically, long-horizon regression were used to evaluate returns *predictability* and *component decomposition* (*e.g.* stationary, drift, and random walk). Early literature includes [Forward Exchange Rates as Optimal Predictors of Future Spot Rates](http://www.jstor.org/pss/1833137) (Hansen and Hodrick, 1980) and [Permanent and Temporary Components of Stock Prices](http://ideas.repec.org/a/ucp/jpolec/v96y1988i2p246-73.html) (Fama and French, 1988). Yet, the apparent intent for use in prediction differs from this precedence.

Instead, ![H](img/08f86bb6e2072ba520c148934f76c0bf.png)-period *future* accumulated log returns are regressed against *lagging* ![H](img/08f86bb6e2072ba520c148934f76c0bf.png)-period eigenvectors from the principal component space:

     ![r_{t+1} + \cdots + r_{t + H} =  \beta_1 \sum\limits_{i = 0}^{H-1} D_{t - i, 1} + \cdots + \beta_k \sum\limits_{i = 0}^{H-1} D_{t - i, k} + \eta_{t + H, H} ](img/3748ef8590a5e71db7a7a168992d56dc.png)

In other words, predict future returns based upon the past. Yet, the past is defined by principal components plus a noise term. One way to better understand this is to consider when ![H = 1](img/a3a8cccd4091f2508770acef6504a71f.png):

     ![r_{t+1}  =  \beta_1 D_{t, 1} + \cdots + \beta_k D_{t, k} + \eta_{t + 1, 1} ](img/1f5b65fdd192860ada78f6e135479ede.png)

Thus, the one-step ahead return is equal to ![\beta](img/e59dd600f7eb22f952e355797bceba2e.png)-scaled *eigenportfolio* from the previous step plus noise. Extending this logic, long-horizon can be interpreted as a longitudinal extension of the eigenportfolio with constant ![\beta](img/e59dd600f7eb22f952e355797bceba2e.png)-scaled weights.

In this interpretation, extending the eigenportfolio longitudinally introduces the advantage of being able to observe the noise ![\eta_t ](img/6568d9b614baea966e0c56010a5e4f80.png) over ![H](img/08f86bb6e2072ba520c148934f76c0bf.png) periods and calculate the hyperplane which simultaneously minimizes the sum of squared residuals over those periods. This insight opens the door to linear machine learning: instead of trying to estimate a single point ![\eta_t ](img/6568d9b614baea966e0c56010a5e4f80.png) (which is pretty tough), a hyperplane can be estimated. Note this interpretation highlights a caveat: predicting accumulated future returns using this model *presumes the noise is stationary for the ![2H](img/6334d77e2c22eedfeb2d94830bf25764.png) period* (provided ![H = T](img/62b925b5f0b638706456da7c94154057.png), if not, then period is ![T + H](img/a61cc2d72b56252da0da844f585fe5b2.png)). Otherwise, the regression assumptions are violated. Hence, duration of ![2H](img/6334d77e2c22eedfeb2d94830bf25764.png) must be sufficiently short for this assumption to be valid.

The trade signal is generated by *assuming mean-reverting convergence* of the residuals ![\eta ](img/0a6837a1d8bde7b09c7d821a74acf002.png) between predicted last ![H](img/08f86bb6e2072ba520c148934f76c0bf.png) period of accumulated log returns versus the actual accumulated returns:

     ![\eta  = [ r_{t+1} + \cdots + r_{t + H} ] - [ \beta_1 \sum\limits_{i = 0}^{H-1} D_{t - i, 1} + \cdots + \beta_k \sum\limits_{i = 0}^{H-1} D_{t - i, k} ] ](img/add048b58ffda2905404fafd927ab1a9.png)

This convergence arises *by construction* from least squares regression estimation of the ![\eta_t ](img/6568d9b614baea966e0c56010a5e4f80.png) hyperplane: residuals are stationary around zero. Thus, divergence from zero at ![\eta_t ](img/6568d9b614baea966e0c56010a5e4f80.png) will converge back to zero at a nearby point.

Or, in trading speak: if actual returns are larger than predicted returns, then assume the corresponding stock is overvalued and sell; otherwise, buy.

*   **Cross Sectional Volatility**

Finally, a *cross sectional volatility* metric ![\sigma_D ](img/caace9246a12cff17c95ed38373b7ec8.png) can be defined within the principal component space ![D ](img/9b99697119ba9275b05e5090634c55ee.png). This metric is a *realized* volatility estimator, namely the [sample standard deviation](http://en.wikipedia.org/wiki/Standard_deviation), of the principal components (![d_{ij} ](img/b54112768e7765389ef782437085089a.png) is the i-th, j-th element in ![D](img/fd6081407ca943a923c743cb5596009a.png)):

      ![\sigma_D(t) = \sqrt{\frac{1}{k - 1} \sum\limits_{j=1}^k {(d_{tj} - \bar{d_t})^2}} ](img/fae01bdf9367a158531383046f9353b5.png)

where the cross sectional mean is defined in the standard way:

      ![\bar{d_t} = \frac{1}{k} \sum\limits_{j = 1}^k d_{tj} ](img/fac7c973eda21f05e6333ed1e0a6dd8c.png)

Hence, coming full circle: ![\sigma_D ](img/caace9246a12cff17c95ed38373b7ec8.png) defines the volatility which is delay embedded to measure volatility-regime correlation, as described in [Delay Embedding as Regime Signal](https://quantivity.wordpress.com/2011/02/24/delay-embedding-as-regime-signal/).