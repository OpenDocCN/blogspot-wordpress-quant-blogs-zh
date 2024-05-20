<!--yml
category: 未分类
date: 2024-05-12 19:25:54
-->

# Quantitative Trading: Do Factor Models Work in the Short Term?

> 来源：[http://epchan.blogspot.com/2006/12/do-factor-models-work-in-short-term.html#0001-01-01](http://epchan.blogspot.com/2006/12/do-factor-models-work-in-short-term.html#0001-01-01)

Besides pair-trading, “factor model” is the most popular workhorse of the statistical arbitrageur. In a previous

[article](http://epchan.blogspot.com/2006/12/market-cap-and-growth-value-arbitrage.html)

, I discussed the most well-known factor model – the Fama-French Three-Factor model, with the general market index returns, the market-cap of the stock, and the book-to-price ratio as the only three factors driving returns. However, as I explained earlier, this factor model has a very long horizon. For the quantitative trader who needs to make money every month, the natural instinct is to look for a more “sophisticated” factor that works in the short term, or even to develop some kind of model that use different factors every month in response to “market condition”. Alas, other than hearsays and second-hand gossips, I have never witnessed an actual success of this approach in a hedge fund or proprietary trading group – at least a success that lasts for more than a year.

I am of course not privy to the current performance numbers of factor models run by some of the most successful hedge funds today. However, there is a class of ETF (called “XTF”) marketed by PowerShares Capital Management that uses a similar factor approach for its stock selection criteria. According to media reports, each stock in these XTF’s is scored by 25 variables such as cash flow, earnings growth, price momentum, etc. This sounds like a classic factor model to me. This model is reportedly designed by the quantitative unit at American Stock Exchange. To find out if they have indeed discovered the holy grail of factor models, I looked at the performance of these XTF compared to their benchmarks.

Here I tabulate the XTF’s for each market cap and value category, their corresponding benchmark market index ETF’s, and finally the YTD differential returns up to December 13, 2006\. (PJG and PJM have too short a history for this comparison.)

|    | **Value** | **Blend** | **Growth** |
| **Large cap** | PWV-IVE=4.8% | PWC-IVV=-3.6% | PWB-IVW=-5.0% |
| **Mid cap** | PWP-IJJ=0.1% | PJG-IJH=N/A | PWJ-IJK=3.1% |
| **Small cap** | PWY-IJS=-0.7% | PJM-IJR=N/A | PWT-IJT=-4.9% |

The differential returns are all over the place: some positive, others negative. To me, this is symptomatic of a factor model that does not have predictive power. (After all, if the differential returns are consistently negative, we could have long the ETF, short the XTF, and make consistent profits!) At the very least, this factor model may have a horizon much longer than what most traders would be interested in – in which case, why not just use the simple Fama-French model?

This is not to say that exotic, proprietary factor models have no use: they tend to be pretty useful for risk management, as volatilities and correlations are often easier to predict than returns. But beware every time your risk management software vendor tries to sell you an alpha generator!