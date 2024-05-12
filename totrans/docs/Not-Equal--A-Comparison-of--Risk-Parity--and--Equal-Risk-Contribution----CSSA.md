<!--yml
category: 未分类
date: 2024-05-12 18:05:44
-->

# Not Equal: A Comparison of “Risk Parity” and “Equal Risk Contribution” | CSSA

> 来源：[https://cssanalytics.wordpress.com/2012/07/19/not-equal-a-comparison-of-risk-parity-and-equal-risk-contribution/#0001-01-01](https://cssanalytics.wordpress.com/2012/07/19/not-equal-a-comparison-of-risk-parity-and-equal-risk-contribution/#0001-01-01)

The term **“Risk Parity”** is often confusing because it is defined and applied differently depending on the firm.  With the advent of multiple variations in tactical asset allocation and indexing strategies, it is perhaps not a stretch to claim that Risk Parity is as vague and elusive  as using the term “hedge fund” to describe a style of investment management. I have created a table below to clarify two different variations that are often used interchangeably and are *not* the same.   A good history of the origins of risk parity can be found here: [http://en.wikipedia.org/wiki/Risk_parity](http://en.wikipedia.org/wiki/Risk_parity). **Systematic Investor**– an excellent blog-  provides some useful R code and testing here: [http://systematicinvestor.wordpress.com/2012/03/19/backtesting-asset-allocation-portfolios/](http://systematicinvestor.wordpress.com/2012/03/19/backtesting-asset-allocation-portfolios/ "risk parity in R"). **Meb Faber**– always a great resource for new ideas- provides an application of Risk Parity to asset allocation as well as a good list of articles here: [http://www.mebanefaber.com/2012/03/22/risk-parity-vs-endowment-model-vs-permanent-portfolio/](http://www.mebanefaber.com/2012/03/22/risk-parity-vs-endowment-model-vs-permanent-portfolio/ "Faber Risk Parity")

In my opinion, it is best to simply consider **Risk Parity** as a broad class of risk-budgeting schemes where the risk of each asset in the portfolio is leveraged (if necessary) to have the same volatility. Essentially, each asset has “equal risk”, and thus the portfolio is considered to be more diversified since returns and risk are less dependent on any one asset. In contrast, **Roncalli** [http://www.thierry-roncalli.com/riskparity.html](http://www.thierry-roncalli.com/riskparity.html "Roncalli")  coins the term **“Equal Risk Contribution” (ERC)**  which is a ***distinct sub-class of Risk Parity*** that seeks to *equalize risk contributions from each asset to the portfolio*. If both methods sound the same after reading various articles, that is because for the often cited two-asset case  they have the same mathematical solution and explanation for their validity. Nevertheless, not all Risk Parity portfolios are the same-  it is necessary to understand the differences between the equal risk and equal risk contribution approach to avoid improper application or interpretation. Below is a table that helps to define the similarities and differences of the two approaches and the relative advantages of each in the context of portfolio allocation.

**Features and Qualities Shared By Equal Risk Contribution (ERC) and Risk Parity (RP)**

| **Algorithm Characteristics** | **Equivalency** | **Equal Risk Contribution (ERC)** | **Risk Parity (RP)** |
| Requires Historical/Expected Asset Returns | ≈ | No | No |
| Considered Heuristic Algorithms That Lack Strong Theoretical Support | ≈ | Yes | Yes |
| Generally Uses Leverage | ≈ | Yes | Yes |
| Generally Uses a Target Portfolio Risk | ≈ | Yes | Yes |
| Allocation Across All Assets in the Universe Selected | ≈ | Yes | Yes |
| Low Turnover Relative to Traditional Models | ≈ | Yes | Yes |
| Comparatively Less Sensitive to Estimation Error than Traditional Models | ≈ | Yes | Yes |
| Generally Superior Return and Sharpe to Equal Weight Portfolios | ≈ | Yes | Yes |
| Better Returns and Sharpe than 60/40 Balanced Stock/Bond Portfolios | ≈ | Yes | Yes |
| Solution for a Two-Asset Portfolio | ≈ | inverse volatility weighted | inverse volatility weighted |
| Conditions for Being Equivalent to Equal Weight Portfolios | ≈ | Equal Asset Volatility and Constant Correlation | Equal Asset Volatility and Constant Correlation |
| Conditions for Being Optimal on the Efficient Frontier | ≈ | Equal Sharpe Ratios and Constant Correlations | Equal Sharpe Ratios and Constant Correlations |

**Features and Qualities That Favor Equal Risk Contribution (ERC)**

| **Algorithm Characteristics** | **Equivalency** | **Equal Risk Contribution (ERC)** | **Risk Parity (RP)** |
| Objective Function | ≠ | volatility of risk contributions=0 | inverse volatility weighted |
| Uses Beta/Covariance Data | ≠ | Yes | No |
| Always Assumes Constant Correlation Matrix | ≠ | No | Yes |
| Holdings Have Equal Risk Contributions to Portfolio Volatility | ≠ | Yes | No |
| Performance Highly Sensitive to the Universe of Assets Selected | ≠ | No | Yes (ie. 5 equities and 1 bond create imbalance) |
| Flexibility of Use for Risk Budgeting and Factor Tilts | ≠ | winner | loser |
| Out of Sample Risk (Given the same target) | ≠ | winner | loser |
| Out of Sample Return (Given the same target or leverage constrained) | ≠ | winner | loser |
| Out of Sample Drawdowns | ≠ | winner | loser |
| Out of Sample Sharpe Ratios | ≠ | winner | loser |
| Out of Sample Diversification (Concentration and Average Correlation) | ≠ | winner | loser |
| Favorable Hybrid Between Minimum Variance and Equal Weight | ≠ | Yes | No |
| Can Be Equivalent to Minimum Variance | ≠ | When Correlation Matrix is Minimized | Not Possible |

**Features and Qualities That Favor Risk Parity (RP) or Equal Risk**

| **Algorithm Characteristics** | **Equivalency** | **Equal Risk Contribution (ERC)** | **Risk Parity (RP)** |
| Simple to Calculate for the Mathematically Challenged (Napkin Factor) | ≠ | loser | winner |
| Intuitively Easy to Understand and Use in Most Software Packages | ≠ | No | Yes |
| Best Sounding Name/Cool Factor | ≠ | loser | winner |
| Practical Use for Dynamic Allocation With Long-Term Monthly Data | ≠ | loser | winner |
| Sensitivity to Covariance Estimation Error | ≠ | loser | winner |
| Generally Requires a Sophisticated Solver for Optimization | ≠ | Yes | No |
| Speed of Calculation for Large Universe | ≠ | Slow | Fast |
| Performance on very large data sets with limited sample size | ≠ | loser (too many covariances relative to sample size | winner (fewer variables to estimate relative to sample size) |