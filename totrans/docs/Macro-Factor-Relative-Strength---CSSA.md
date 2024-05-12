<!--yml
category: 未分类
date: 2024-05-12 18:11:24
-->

# Macro-Factor Relative Strength | CSSA

> 来源：[https://cssanalytics.wordpress.com/2011/04/02/macro-factor-relative-strength/#0001-01-01](https://cssanalytics.wordpress.com/2011/04/02/macro-factor-relative-strength/#0001-01-01)

Most quantitative traders and investors love the concept of momentum or relative strength based investing. The reasons are obvious: 1) it makes intuitive sense that more money is made switching into stocks that have the highest compound growth rate 2) even the crustiest and most cynical academics concede that it is a real anomaly 3) it is a lot easier for the average person without serious trading infrastructure to implement. On all of these points, I wholeheartedly agree– It is a durable anomaly that is likely to last for a long time.

That said, it is my humble belief that the market has gotten more complex and that the momentum trade in its simplest form is temporarily a crowded trade. I also believe more importantly that the current state of the world is driven by larger forces such as interest rates, currencies and commodities. In a stable decade where investors are optimistic– such as the 90s, it is possible for the simplest of momentum strategies to thrive since they depend on investor feedback loops and money flow. As money pours into the market chasing themes, the waves gather momentum and build up to tremendous heights. Such periods are marked by low correlations between stocks and large divergences in the performance of certain styles versus others (think of how much better growth did than value). Stocks tend to live in their own worlds so to speak– driven by their own fundamentals or story– and hence unsystematic risk is more prevalent than systematic risk.  In an unstable decade,  we see the opposite situation: correlations between stocks are high–reflecting the predominance of systematic risk versus unsystematic risk. Capitalizing on temporal dispersion discrepancies is a valid way to reconcile such issues, but is not the topic of this post. In such decades- like the one we have been in since 2001 or 2002-  the shift in macroeconomic factors is a significant driver of returns, and tends to explain the winners and losers more clearly, but unfortunately after the fact.

The way to reconcile this issue is to naturally create a relative strength model that is based on such macro factors. After all, academics have shown that industry and style-based relative strength are very useful– so why not look at factors such as commodity , interest rate, currency, and country exposure?  Much of the original logic for such a model was based on APT – or arbitrage pricing theory. I had a fine conversation with  Richard Roll (the creator of APT) many years ago, who is not just an academic but has worked at Goldman Sachs and also heavily involved in asset management. He instilled the virtue and logic of the APT approach, and while its intuitive appeal was never lost upon me–a practical implementation certainly was. Back in the day, you used APT to create a regression model that incorporated macro factors to predict stock price movements. Of course, like many regression-based approaches, the predictions were too noisy to generate significant alpha.

It occured to me that the solution is to merge the wonderful concept of relative strength with such an approach– but the question is how? The answer is that you can use regression to determine how responsive a given stock is (or ETF) to various factors, and then look at the relative strength of those factors to generate a dynamic score. In this case, thanks to the world of ETFs this is very easy to do. Imagine that I was to look at Exxon Mobil (XOM) and I wanted to decompose its returns into major macro factors using ETFs. The result might look something like this (although this is a fictitious example):

US Dollar (UUP): 13%

S&P500 (SPY): 30%

Oil (USO): 42%

Natural Gas (UNG): 15%

10-year bond (IEF): -20%

Credit spreads(HYG-IEF): 20%

From this example we can derive a lot of information from which to create a score for Exxon. We might look at the relative strength of the underlying ETFs in order to create a macro-factor relative strength ranking. The weightings would be derived from the factor exposure above. Using this model, we can rank every stock in the stock market without knowing the relative performance of a given stock versus the universe. This is accomplished by running relative strength algorithms on the macro factors only to determine which are most significant and then using these ranks to apply to each stock’s factor exposure.

The resulting model still uses relative strength– but in a very interesting new way. Perhaps this method might be a nice complement to existing relative strength models based purely upon cross-sectional price momentum.