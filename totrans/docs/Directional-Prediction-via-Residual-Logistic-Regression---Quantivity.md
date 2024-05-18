<!--yml
category: 未分类
date: 2024-05-18 13:55:03
-->

# Directional Prediction via Residual Logistic Regression | Quantivity

> 来源：[https://quantivity.wordpress.com/2009/12/27/directional-prediction-via-residual-logistic-regression/#0001-01-01](https://quantivity.wordpress.com/2009/12/27/directional-prediction-via-residual-logistic-regression/#0001-01-01)

Paul Teetor wrote a nice study on [Predicting Swap Spreads](http://quanttrader.info/public/predictingSwapSpreads.pdf). Worth noting is his use of [logistic regression](http://en.wikipedia.org/wiki/Logistic_regression) to predict *probabilistic direction* of next period spreads based upon *residuals* calculated from a linear model of the historical spread. In other words, Paul is evaluating the following logical hypothesis (synthesized from p. 5):

> Can the future direction of swap spreads be predicted using their historical mispricings from fair value, as estimated from influential market data (treasury notes, interest rate swaps, LIBOR, BIX, SPX).

Provided robust directional prediction, a profitable trading strategy can be defined as (p. 22):

   *Long*: if P(up) > 0.5, go long today
   *Short*: if P(down) > 0.5, go short today

This methodology is particularly interesting as it is *equally applicable to many other financial instruments*, provided suitable notions of “mispricings” and value estimators. For example, directional prediction of co-integrated pairs can be similarly estimated, extending the analysis introduced in [Mean Reversion](https://quantivity.wordpress.com/2009/07/19/mean-reversion/).

Generic applicability arises from two aspects of this methodology:

*   Directional prediction: logistic regression is used to estimate the probability of spreads either rising or falling, thus a *directional change*, rather than numeric values
*   Residuals: explanatory variable of the logistic regression are residuals from a linear regression, demonstrating another [wonder of residuals](https://quantivity.wordpress.com/2009/08/02/wonder-of-residuals/)

The following steps outline this methodology, and how to translate into a mechanical trading system:

1.  Estimate fair value (p. 14): estimate the fair value of the swap spread via a linear regression using market data known by traders to be relevant to swap spreads (treasury notes, interest rate swaps, LIBOR, BIX, SPX)
2.  Calculate “mispricings” (p. 16): calculate the difference between observed and estimated fair value of the swap spread, generating residual series (note they exhibit serial dependence when plotted against time, indicating they may potentially possess temporal explanatory power)
3.  Estimate directional probability (p. 19): estimate two logistic regressions, one for “buy model” and one for “sell model”, each of whose dependent variable is log of the directional probability (*i.e.* increasing or decreasing spread) and independent variable is “mispricings” residuals
4.  Evaluate significance (p. 20): evaluate significance of ![\beta](img/e59dd600f7eb22f952e355797bceba2e.png) for both logistic regressions; if significant, then the “mispricing” residuals have power in predicting future direction of spreads
5.  Build trading system (p. 22): provided significant directional prediction, generate the corresponding long/short daily trade entry rules

Note: for those interested in technical indicators, Paul also incorporates momentum and acceleration indicators in his analysis (see p. 6). Use of these indicators is unrelated to the above methodology discussion, and thus is omitted from this post for brevity.