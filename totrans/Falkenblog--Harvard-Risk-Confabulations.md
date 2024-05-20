<!--yml
category: 未分类
date: 2024-05-12 20:32:04
-->

# Falkenblog: Harvard Risk Confabulations

> 来源：[http://falkenblog.blogspot.com/2012/04/harvard-risk-confabulations.html#0001-01-01](http://falkenblog.blogspot.com/2012/04/harvard-risk-confabulations.html#0001-01-01)

John Campbell is one of the world's most esteemed financial economists, which means that he publishes very rigorous and well-received papers showing that some strange result is a function of risk, even though that risk metric is totally nonintuitive. Case in point, Campbell, Giglio, Polk, and Turley (2012) have a paper entitled

[An Intertemporal CAPM with Stochastic Volatility,](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=2021846)

and find that

> the negative post-1963 CAPM alphas of growth stocks are justified because these stocks hedge long-term investors against both declining expected stock returns, and increasing volatility.

Consider the following correlation between the stock market (Rm-Rf) and changes in the VIX, using monthly data from 1986-2012:

[![](img/6d5975f6a0923263d39f07fb6ff67f05.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgK8DS42CMYY2SB5PduN0G11xmz6xqZjH0urHoXNqkbc12LGXQfe6w61wRWdTI9JXv0mJ5OMSJWEPkkwBnFh2FQ8WnL6ohKN2UWu7NaeNkEWAAkeGtMGg8YUy1yFw9LFszm748PkQ/s1600/rmvix.tif)

There's a nice negative relation, because volatility rises when markets tank and vice versa. This is why you hedge market exposure being long the VXX, the VIX ETF (though, you

[pay a lot](http://falkenblog.blogspot.com/2012/03/vxx-expensive-again.html)

for that!).

Now consider the relation between the HML or '

[value risk proxy portfolio](http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html)

', which is ever so slightly positively correlated with the VIX index, suggesting that

value

stocks have the insurance-like property of doing better in more volatile periods.

[![](img/580aa7578eb31f055e07ff37679170ec.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjIKoWC1VyUWJmdOpARZmz7gU6GiZaRz4g9yaC-lHuOrD31lVZ2Nq_UqKqewCl7_pW_oGHQtjJmpq5w68QN6lajTslmVSjQgDMGVzg2fvmaDG8-Bc4vCu0l_s1DPDZlBxgD86k9Ow/s1600/hmlvix.tif)

That is, value, not growth, does better when volatility rises, but more importantly, the the R

²

for this value portfolio is only 2% vs 50% for a regression of the market on VIX changes. One would think you can't get blood out of that stone, that if the positive market risk premium has a large negative weight, then something with a small positive effect would not explain the value effect. Then again, you are probably not familiar with the powerful modern econometric methods that economists sling around.

First they take 6 time series (aggregate market, stock variance, aggregate P/E ratio, yield curve spread, a value portfolio, and the Baa-Aaa yield spread) and create a Vector Auto Regression. This VAR is used to estimated returns and volatility that are used to estimate how much risk value/growth portfolios have. This method uses a closed form (!) solution to a model that uses the 'risk aversion coefficient', which is great because it gives you another free parameter, and is a neat mathematical trick. Campbell et al. casually note "the empirical implementation of our model is a success," because there exist "reasonable preference parameters that would make a long-term investor" not jump into value stocks even though they seem to generate a return premium.

So, a model with totally non-intuitive metrics for stock return premiums and volatility risk factors can explain the value premium given certain unobserved parameters. Stock return premiums and volatility by themselves, however, do not explain anything.

Given my understanding of finance and macro, I am highly suspicious of string theorists who claim their model works great because if you give academics any set of stylized facts (eg, the value effect, the basic facts of physics), more math can explain it, confidently so. Following the confabulatory research I

[have been touting for weeks,](http://www.amazon.com/Whos-Charge-Free-Science-Brain/dp/0061906107/ref=sr_1_1?s=books&ie=UTF8&qid=1331592463&sr=1-1)

they will consider something a success as long as it can rationalize their prejudices, which isn't too hard.