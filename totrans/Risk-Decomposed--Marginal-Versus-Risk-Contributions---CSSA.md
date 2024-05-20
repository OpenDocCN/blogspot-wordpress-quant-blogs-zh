<!--yml
category: 未分类
date: 2024-05-12 18:06:09
-->

# Risk Decomposed: Marginal Versus Risk Contributions | CSSA

> 来源：[https://cssanalytics.wordpress.com/2012/07/10/risk-decomposed-marginal-versus-risk-contributions/#0001-01-01](https://cssanalytics.wordpress.com/2012/07/10/risk-decomposed-marginal-versus-risk-contributions/#0001-01-01)

In today’s environment more than ever, risk attribution is becoming critical to understanding portfolio composition. It is more important to understand how much risk we are effectively betting on a given position as it is to create a prediction for the return of that position. Incorrect position sizes (look up the London Whale) can turn a positive expectation into a negative proposition at the portfolio level. But how do we determine risk in a portfolio context? The traditional method of decomposing risk looks at both marginal and risk contributions for the assets contained in the portfolio.

First, lets define what marginal contributions are in contrast to risk contributions. The concept of marginal is central to economics, and considers the unique impact of a change in a variable in the context of a complex system. It is essentially a derivative that measures the rate of change in some measure of interest given a small change in a variable. An example might be studying what if any impact further quantitative easing would have on the economy.  But what about the marginal contribution of an asset to portfolio risk? For some reason, this concept is poorly explained and the notation is often inconsistent. In English, the marginal risk contribution (MRC) of asset A (lets call this “a”) to the portfolio (which contains asset A) is equal to:

**MRC**= correlation of asset A to the portfolio  x the standard deviation of asset A

or alternatively (Ca/p) x (SDa)

The marginal risk contribution can more intuitively be expressed using a concept many of us are all familiar with– Beta.  It is conventional to judge the risk of a given security by its “Beta” to a given stock index. Often the example is given that we can estimate the % change of a stock on a given day by multiplying the beta of that stock to the index to the % change of the index. In other words, if we look at a stock that has a beta of 2 to the S&P500 and the S&P500 goes up 1% tomorrow, then the stock should probably go up 2% (2x 1%). Often the stock in question is actually a member of the S&P500 index. This makes the MRC easy to understand. In this case we want to understand how the stock might increase portfolio risk given a small change in the allocation to that stock. That is, what is the rate of change in S&P500 risk given a change in the value of one of its holdings. The alternative formulation is:

**MRC**= Beta of asset A x Standard Deviation of the Portfolio

or (Ba/p) x (SDp)

Note that this implies that the the marginal risk contribution can actually be negative, which would suggest we increase the weight of that asset in the portfolio. From a risk management standpoint, it is desirable to equalize marginal risk contributions from assets in  the portfolio so that small changes in the value of each asset would have the same impact on  portfolio risk (in terms of the rate of change). However, this concept can border on the ridiculous since anything other than a small change would concentrate the risk of the portfolio in the assets that have the largest  risk contribution.  So how do we measure the risk contribution of an asset (RC)? As it turns out, the answer is quite simple:

**RC= **the % weight of asset A in the portfolio x Beta of asset A x Standard Deviation of the Portfolio

or Wa x (Ba/p) x (SDp)  OR  Wa x (Ca/p) x (SDa)

OR even simpler-  **RC=   Wa x MRC**

Note that the Portfolio Risk (SDp)= RC(a)+ RC (b)+…………….RC (n)

In other words, the portfolio risk/standard deviation is the sum of the risk contributions from each asset.

For example, if I  am running a hedge fund  and I  hold 25% of my portfolio in the stock Bank of America, and it has a Beta to the portfolio of 3 and the portfolio has a standard deviation of 10%, then the RC=  .25 x 3 x 10%= 7.5%

This means that 75% of my portfolio risk is going to be dictated by what happens to Bank of America– if it goes up, I make a lot of money, if it goes down the portfolio will also tank. It doesn’t take a genius to see that this means that the risk is too concentrated in one stock. In practice, it is desirable to spread out total risk contributions across as many stocks or assets as you can in the most equivalent manner. This is one way to look at diversification– spreading out your effective bets in a way that has as little concentration risk as possible. The concept of diversification has more than just this one element–but that is a topic for a future article.

These risk attribution concepts are also central to optimization using traditional approaches such as minimum variance, risk parity, maximum diversification, and mean-variance. All of these methods positioned in the form of unconstrained solutions (long and short) require an equalization of either marginal or risk contributions.Lets preview how some traditional optimization methods address risk. This will be addressed in further detail with my forthcoming paper on the “**Minimum Correlation Algorithm**.”

**Minimum Variance**–  the marginal risk contributions are equivalent

**Mean-Variance**– the marginal sharpe ratios are equivalent

**Risk Parity** (see ERC by Roncalli [http://www.thierry-roncalli.com/download/erc-slides.pdf](http://www.thierry-roncalli.com/download/erc-slides.pdf) )- the risk contributions are equivalent

**Max Diversification** (See Choueifaty [http://www.iijournals.com/doi/abs/10.3905/JPM.2008.35.1.40](http://www.iijournals.com/doi/abs/10.3905/JPM.2008.35.1.40))- the marginal correlations are equivalent.    (*Note that this is functionally equivalent the* ***Minimum Correlation Portfolio*** *but is different than the **Minimum Correlation Algorithm***:  [https://cssanalytics.wordpress.com/2011/08/09/forecast-free-algorithms-a-new-benchmark-for-tactical-strategies/](https://cssanalytics.wordpress.com/2011/08/09/forecast-free-algorithms-a-new-benchmark-for-tactical-strategies/)

Note that in long only versions of these methods (with the exception of risk parity) the feature of equal marginals or risk contribution no longer holds. However, these algorithms seek to find the best solution without short-selling that often produces nearly equivalent values.