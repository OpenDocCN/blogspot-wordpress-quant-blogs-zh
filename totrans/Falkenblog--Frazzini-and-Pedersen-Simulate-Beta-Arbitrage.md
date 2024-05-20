<!--yml
category: 未分类
date: 2024-05-12 21:13:52
-->

# Falkenblog: Frazzini and Pedersen Simulate Beta Arbitrage

> 来源：[http://falkenblog.blogspot.com/2010/12/frazzini-and-pedersen-simulate-beta_15.html#0001-01-01](http://falkenblog.blogspot.com/2010/12/frazzini-and-pedersen-simulate-beta_15.html#0001-01-01)

[Andrea Frazzini and lasse Pedersen](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1723048)

have a paper out entitled 'Betting against Beta'. It has an insane number of tables and figures at the end, which is nice because its all there if you care to look, and with electronic publishing, no polar bears are killed in the process. They take the finding that 'risk does not appear positively related to return within asset classes, and form Betting-Against-Beta portfolios by going long the low beta assets, and short the high beta assets. Specifically:

> A BAB factor is long a portfolio of low-beta assets, leveraged to a beta of 1, and short a portfolio of high-beta assets, de-leveraged to a beta of 1\. For instance, the BAB factor for U.S. stocks achieves a zero beta by being long $1.5 of low-beta stocks, short $0.7 of high-beta stocks, with offsetting positions in the risk-free asset to make it zero-cost

They find significant returns to betting against beta within 19 country's equity markets, and also look at US treasuries, and credit markets.

Another brick in the wall showing that covariance with 'the market', any market, is not cross-sectionally related to returns. Now, it could be 'expected returns' were correlated with this conditional covariance, and all we have are realized returns, but at what point does one

[give up on this line of reasoning](http://seekingalpha.com/article/160413-expected-returns-are-they-unmeasurable)

?

As to the question why, Frazzini and Pedersen argue it is related to margin requirements. That is, a higher margin requirement inhibiits leverage, and this causes one to prefer high beta assets to get more bang for your buck. While this works in this model, it predicts people should be massively invested in the stock market, but average stock market holdings are comparable to household's investment in automobiles. Only 15% of the population hold stocks directly (not via pensions), and stocks are only about

[50% of their financial assets](http://www.ecb.int/events/pdf/conferences/ecb_cfs_conf/Lucas.pdf?2511523074ffd7b4feb7d199e141a1ea)

(other being bonds and cash). So, if the margin was a binding constraint, this is a major counterfactual.

Sure, increasing haircuts (margins) hurts prices, but usually these are stressed markets, a highly biased samples for a general inference. Consider that eliminating shorting on certain stocks usually provides a one-day increase in the stock price, but over time, it is not obvious countries with more onerous short selling restrictions are more overpriced in aggregate.

If investors are leverage constrained, and so favor high beta assets or low beta assets, leading to lower returns of high beta assets, low volatility portfolios being offered now are clearly dominant portfolios. If at least some investors are not constrained, this is not an equilibrium, because they will all strictly prefer the low volatility portfolios.

As to the Treasury-Eurodollar spread predicting equity BAB portfolios, to the extent there is beta compression in stressed times, that isn't really interesting. Now, if the prospective returns are predictable, that would be interesting. Alas, with time series on a factor, there's never enough data, and I've never seen anything work well out-of-sample.

My favorite explanation for the risk-return pattern--flat as a first approximation, negative for the highest risk assets in any class--is that 1) as investors measure risk relative to a consensus benchmark, no risk premium exists and 2) the really high risk assets are overpriced due to dupes who think they all have alpha. The latter is kind of a margin story, and it is a disequilibrium one.