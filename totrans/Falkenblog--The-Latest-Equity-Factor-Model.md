<!--yml
category: 未分类
date: 2024-05-12 21:48:25
-->

# Falkenblog: The Latest Equity Factor Model

> 来源：[http://falkenblog.blogspot.com/2009/09/latest-equity-factor-model.html#0001-01-01](http://falkenblog.blogspot.com/2009/09/latest-equity-factor-model.html#0001-01-01)

[Lu Zhang](http://www.bus.umich.edu/Academics/Departments/Finance/Finance/FacultyBio.asp?id=000798900)

and Long Chen have an article that seems to be making quite a stir:

[A Better Three-Factor Model that Explains More Anomalies](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1418117)

. The current champion Three-Factor model is the Fama-French model that has three factors: size, value, and the market. The value factor is created by going long value stocks (high book-market, low P/E) and short growth stocks (low book-market, high P/E). The size factor is long small cap, and short large cap. Size and growth are cross tabbed in the Fama-French approach, to maximize their independence. The market factor is the value-weighted market return minus the risk free rate.

Now, Fama and French created this model to explain, well, itself. In 1992 they noted that value, and size, were outside the traditional CAPM, that had merely the market as a factor. So, adding a size and value factor, explained stocks sorted by value and size. If that seems like an anomaly explaining itself, welcome to Modern Finance, where return is a function of risk, which is a function of return. It's like explaining high productivity growth by saying a country has a high

[Solow residual](http://en.wikipedia.org/wiki/Solow_residual)

. Anyway, these are the most prominent exceptions to the CAPM, around since around 1980, and observable in most countries. The value effect has remained strong since first discovered, while the size effect has subsequently been pretty small.

But there are new anomalies to this model. One anomaly is the

[capital issuance anomaly](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=251502)

, where issuers of capital--debt or equity--tend to underperform, while those who buy it back tend to outperform. It seems either insiders are prescient, or outsiders are consistently poor market-timing investors, or companies tend to burn money when they ask for for new investments they can not, or are not willing, to finance themselves. Another anomaly is cash-flow/assets, first documented by

[Houge and Loughram](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=886093)

: firms with high cash-flow/assets outperform, firms with low cash-flow/assets underperform. Another is

[momentum](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=299107)

: firms with high past returns over the past 6-18 months tend to outperform over the next 6-18 months, the opposite for the low returning stocks. Also, firms with high

[asset growth](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1360680)

tend to underperform, firms with low asset growth tend to outperform. A lot of this is the internet bubble, because firms that got a lot of assets through acquisitions, or issuing new shares, did worse than those that did not, and this is obviously related to the equity issuance anomaly. Lastly, firms with

[higher distress](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=917567)

, as measured by a metric of default, do worse than firms with lower distress. Basically, outperforming firms tend to be firms one would think are good companies even if you did not know what the valuation was: high profits, low default rates.

Now, Zhang and Chen identify two new factors to replace value and size. The first is Investments-to-Assets. This is the change in Property, Plant and Equipment plus the change in inventories over assets. Firms with high I/A ratios have higher returns than those with low I/A ratios. Their other factor is Net Income minus Extraordinary Items divided by assets. Firms with higher ROAs do better than those with lower ROAs.

Clearly, their new factors are derived from the existing anomalies, as I/A and ROA are going to be correlated with distress metrics, asset growth, capita issuance, in straightforward ways. So in that sense, the fact this new approach can 'explain' those anomalies is rather unsurprising, in the same way that a value factor explaining the value anomaly is unsurprising. What is surprising is these factors do a better job at explaining the size and value portfolios than the value and size factors. Further, it does a better job explaining momentum portfolio returns.

Zhang and Chen argue this is a direct implication of Tobin's Q-theory, noting it is "potentially consistent with the risk hypothesis". Their basic argument is that firms that have high ROAs necessarily have higher discount rates, otherwise they would have more assets. Thus of course they have higher returns, because they have higher discount rates. If they had lower discount rates, they would issue more equity (because it would be cheap to issue), and increase their assets, lowering their ROA. One could also argue firms with higher momentum have higher returns because they have higher discount rates, and this is autocorrelated.

I argue the 'risk hypothesis' is demonstrably false, and present a theoretical argument why (see SSRN paper

[here](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1420356)

, book

[there](http://www.amazon.com/Finding-Alpha-Search-Return-Finance/dp/0470445904/ref=pd_rhf_p_t_1)

). The problem with their explanation is that it doesn't have the right covariances with intuitive metrics of aggregate welfare, things like 'the market', or GDP growth, etc. Risk is theoretically all about correlation to our Stochastic Discount Factor, and if only mere characteristics proxy risk, it seems highly dubious. One can argue, correlations and covariances are all backward looking, at characteristics like Inv/Assets and ROA are more forward looking, but when you form portfolios based on these characteristics and look at their correlations in real time over the past 80 years, the correlations still don't work.