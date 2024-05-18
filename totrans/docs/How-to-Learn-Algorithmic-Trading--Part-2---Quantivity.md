<!--yml
category: 未分类
date: 2024-05-18 13:53:30
-->

# How to Learn Algorithmic Trading: Part 2 | Quantivity

> 来源：[https://quantivity.wordpress.com/2010/01/12/how-to-learn-algorithmic-trading-part-2/#0001-01-01](https://quantivity.wordpress.com/2010/01/12/how-to-learn-algorithmic-trading-part-2/#0001-01-01)

Excellent readership and thoughtful comments on the original [How to Learn Algorithmic Trading](https://quantivity.wordpress.com/2010/01/10/how-to-learn-algorithmic-trading/) have motivated two follow-up posts on learning quantitative / algorithmic trading (while retrospectively revising the original to improve consistency). This Part focuses on the cross-discipline foundations of financial mathematics, whose knowledge is generally assumed by practitioners and financial modeling literature. The subsequent, Part 3, focuses on [modern financial modeling and analysis](https://quantivity.wordpress.com/2010/01/12/how-to-learn-algorithmic-trading-part-3/).

Depending on reader interest, this topic may warrant a future series of posts to delve into seminal literature in selected trading disciplines, such as suggested by [etrading](http://etrading.wordpress.com/2010/01/11/quantivity-on-learning-algo/) on the [Penn-Lehman Automated Trading Project](http://www.cis.upenn.edu/~mkearns/projects/plat.html).

Thanks to [awwthor](http://awwthor.wordpress.com/), quant.this, [Josh Ulrich](http://blog.fosstrading.com/), [Gappy](http://www.twitter.com/gappy3000), and Bjørn for their comments and recommendations. As with the original post, the following is intended to inform *retail quantitative trading with a bias to equity, exchange-traded derivatives, and FX*.

To begin, start with solid theoretical econometrics, with emphasis on time series, and meet regression (assuming solid background in linear and matrix algebra):

*   Time Series Analysis, by Hamilton: classic text on time series econometrics
*   Econometric Analysis, by Greene: classic text on theoretical econometrics

Next, dive into filtering and wavelets and meet Fourier:

*   Wavelet Methods for Time Series Analysis, by Percival and Walden: standard theoretical text on wavelets
*   A Wavelet Tour of Signal Processing: The Sparse Way (3rd Ed), by Mallat and Peyré: applied filtering and wavelets for finance and economics

Explore modern statistical / machine learning and meet reinforcement and (un)supervision, descendant of original Turing / von Neumann “AI” tradition:

*   Artificial Intelligence: A Modern Approach, by Russell and Norvig: standard introduction to classic AI
*   The Elements of Statistical Learning, by Hastie, Tibshirani, and Friedman: standard intermediate statistical learning
*   Pattern Recognition and Machine Learning, by Bishop: intermediate classification and learning
*   Pattern Classification, by Duda: standard introductory classification

Review operations research and meet duality, with focus on mathematical optimization (not to be confused with computer science “programming”); thanks to [Gappy](http://www.twitter.com/gappy3000), since my references pre-date many of these:

*   Linear and Nonlinear Programming, by Luenberger: standard introduction to optimization
*   Nonlinear Programming, by Bazaraa *et al.*: standard non-linear optimization
*   Convex Optimization, by Boyd and Vandenberghe: standard convex optimization (generalization of linear methods, including LP, OLS, *etc.*), including approximation, fitting, and estimation

Finally, for those interested in options and vol, review modern stochastic calculus and meet Itō (presuming working knowledge of measure theory and stochastic processes):

*   Financial Calculus, by Baxter and Rennie: pleasant intuitive introduction
*   Stochastic Calculus for Finance I, by Shreve: gentle introduction via binomial
*   Stochastic Calculus for Finance II, by Shreve: gentle continuous-time introduction

Continue on to [Part 3](https://quantivity.wordpress.com/2010/01/12/how-to-learn-algorithmic-trading-part-3/) to dive into modern financial modeling and analysis.