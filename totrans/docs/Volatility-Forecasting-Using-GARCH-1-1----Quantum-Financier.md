<!--yml
category: 未分类
date: 2024-05-18 14:04:13
-->

# Volatility Forecasting Using GARCH(1,1) – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2010/08/26/volatility-forecasting-using-garch11/#0001-01-01](https://quantumfinancier.wordpress.com/2010/08/26/volatility-forecasting-using-garch11/#0001-01-01)

Continuing on the current series of post, I was at the point of forecasting volatility. There is several ways to just that; this very topic is the subject of a lot of research in finance. Different models to model volatility are available and they range from both ends of the complexity spectrum. I am going to be using what I think is one of the most popular: the GARCH(1,1). Just as a side note however, I don’t think it is the best model to use, but I do think that the simplicity of it makes it very attractive. For the more sophisticated quant crowd, in the GARCH family, the EGARCH seems to better forecast market volatility than its counterparts. I will not go into to much detail on the GARCH process (ie this is not meant to be an introduction post), if you would like to hear more about it, please let me know in the comment section.

For SPY since 2000, here is what a GARCH(1,1) model looks like, plotted vs the 21 day standard deviation with the residuals at the bottom. Results have been created using the tseries and quantmod libraries for R.

[![](img/de07b3d8f5203d3b407dd8c6a75372ec.png "garch(1,1)")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/08/garch11.png)

In terms of significance, the model significantly filtered the ARCH effect and the conditional normality assumption does not seem to be violated (using Jarque Bera and Box-Ljung tests). Regardless of the textbook testing, eyeballing the chart, we see that the model is fairly good at predicting SPY’s volatility. Now that we have the model in place, the next post should be on how to use a similar model on volatility of volatility once it has been stripped of its correlation with the actual volatility to see if we can improve our trading results and especially our regime switching strategies.

QF