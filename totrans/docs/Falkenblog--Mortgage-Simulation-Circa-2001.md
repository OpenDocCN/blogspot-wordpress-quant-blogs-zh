<!--yml
category: 未分类
date: 2024-05-12 22:46:15
-->

# Falkenblog: Mortgage Simulation Circa 2001

> 来源：[http://falkenblog.blogspot.com/2008/11/mortgage-simulation-circa-2001.html#0001-01-01](http://falkenblog.blogspot.com/2008/11/mortgage-simulation-circa-2001.html#0001-01-01)

In this latest crisis, one thing that really intrigues me is the degree to which

[everyone underestimated](http://falkenblog.blogspot.com/2008/10/endogenous-failure-in-complex-systems.html)

mortgage credit risk. I was oblivious, doing other things, but what were those in this sector thinking? I am skeptical of most of those who loudly claim to have foreseen this crisis for

[several reasons](http://www.overcomingbias.com/2008/11/beware-the-pres.html)

and I won't rehash them. But this

[piece estimating mortgage credit risk](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=295633)

in 2001 highlights a common error in risk management, or econometric analysis:

> To estimate the empirical survival curves, we rely on a large and geographically diverse data set from a major financial services firm. Data includes credit ratings for the borrower at the time of loan origination. Inclusion of this important variable helps ensure unbiased estimation of the coefficients of other risk factors, such as current loan-to-value ratio and changes in local unemployment rates. We should also acknowledge data limitations: it only includes loans originated during 1993-1997 time period when house prices in most (though not all) markets were stable or increasing

Sounds great, like they are just modeling cross-sectional risk, dipping their toe in the empirical pool. After all, 4 years, not including any cyclical volatility, that would be irrelevant for modeling a worst-case-scenario, and they realize this.

But then after torturing the data for 30 pages, the authors conclude with:

> We find that the current regulatory standards for capital are too high in most cases.

No mention in the conclusion about the lack of a real cycle in their sample data! They knew the data's limitations, but by the end ignored them. In other words, forget about the business cycle--we have a large number of observations! I see this a lot in default modeling, where someone will look at a bunch of daily data on bonds, and say they have 400,000 observations in the default model, ignoring the fact that the ten years of daily IBM data is not 2520 observations, more like 3.

It's a common problem, mistaking the number of observations for degrees of freedom, because the correlation structure underlying the data may actually drastically reduce the degrees of freedom. Making sure your data has the appropriate sample is a big issue in all social science, as often someone will observe how college kids respond to stimuli to predict how people in general respond, assume men are the same as women. Their is no simple cure other than to be thoughtful about the specific application.