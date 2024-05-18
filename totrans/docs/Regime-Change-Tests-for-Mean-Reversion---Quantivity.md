<!--yml
category: 未分类
date: 2024-05-18 13:56:04
-->

# Regime Change Tests for Mean Reversion | Quantivity

> 来源：[https://quantivity.wordpress.com/2009/08/15/regime-change-tests-mean-reversion/#0001-01-01](https://quantivity.wordpress.com/2009/08/15/regime-change-tests-mean-reversion/#0001-01-01)

An institutional algo trader recently posed the following question:

> Q: So I have data that is mean reverting, but then the mean changes…What are the best tests for me to see when that is happening?

As always, there is no single “correct answer”. Answering this question depends upon broadly generalizing the previous post on [Quantile Stability](https://quantivity.wordpress.com/2009/08/03/stability-by-quantile/).

Applicable detection methods depend upon the interpretation of “mean changes” in this context. Factors to potentially consider in this context include:

*   Signal origin (type and construction)
*   Model linearity
*   Discontinuity form (linear or non-linear)
*   Desired detection frequency

Discontinuity owing to parametric stability benefit from techniques analyzing estimation and decomposition. Low dimensional, linear time-series discontinuities can be detected using classic econometric structural change methods (Chow, Quandt, CUSUM, et al). Quantile regression may be effective for evaluating non-time continuity / stability of parametric linear models. Higher dimension, non-linear time-series discontinuity may be detected using [wavelet](http://en.wikipedia.org/wiki/Wavelet) decomposition. All of these methods can be made pseudo-adaptive, at nearly any frequency, by using the corresponding iterative algorithmic form.

Discontinuity owing to variance or covariance stability benefit from techniques analyzing covariance structure. A very wide variety of techniques are available in this domain, most commonly including: variance-derived tests (e.g. variance ratio to [ACF](http://en.wikipedia.org/wiki/Autocorrelation_function)), orthogonal / orthonormal decomposition techniques (e.g. [PCA](http://en.wikipedia.org/wiki/Principal_component_analysis) or [ICA](http://en.wikipedia.org/wiki/Independent_component_analysis)), and [[G]ARCH family](http://en.wikipedia.org/wiki/GARCH). [Stochastic volatility](http://en.wikipedia.org/wiki/Stochastic_volatility) models are common in derivative disturbance models.

Depending on methodology, readers may wish to consider modeling the discontinuities or disturbances. Standard disturbance / residual models include such techniques as [state space models](http://en.wikipedia.org/wiki/State_space_(controls)) (generalization of linear filters, such as Kalman).

Subsequent posts will dive into practical use of each of these techniques within the context of quantitative trading.