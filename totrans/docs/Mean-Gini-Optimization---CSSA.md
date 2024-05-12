<!--yml
category: 未分类
date: 2024-05-12 18:06:47
-->

# Mean-Gini Optimization | CSSA

> 来源：[https://cssanalytics.wordpress.com/2012/02/25/mean-gini-optimization/#0001-01-01](https://cssanalytics.wordpress.com/2012/02/25/mean-gini-optimization/#0001-01-01)

In the last post we introduced the Gini Coefficient as a measure of inequality and statistical dispersion. The primary benefit to using the Gini versus standard deviation is the proper consideration of abnormally large values in the cumulative distribution. There are many applications of the Gini within quantitative finance. One example is the Mean-Gini framework, which was presented as an alternative to classic Mean-Variance optimization. So what are the advantages of a Mean-Gini framework? Cheung et al. (2007) provide a very compelling argument:

“From a theoretical perspective, the mean-variance approach is appropriate
only when investment returns are normally distributed or investors’ preferences can be
characterized by quadratic functions.As the assumption of quadratic utility is known to be problematic on theoretical grounds, normality of investment returns becomes necessary for the mean-variance approach to hold. The validity of the assumption of normality or even near normality, however, is questionable when applied to ﬁnancial assets such as derivatives (which include various forms of options on stocks and other assets), stocks from emerging markets,and hedge funds.”

Given that we know financial data has a tendency to “mis-behave” (the 1 in 10 trillion events using normal distribution assumptions that happen every 10 years), the Mean-Variance framework is clearly more fragile than a Mean-Gini framework. That is the good news, unfortunately the bad news is that the use of the Gini Coefficient for optimization is complex and there is no efficient closed-form solution such as the case for the Markowitz Mean-Variance framework. In fact, the calculation and interpretation of the Gini Coefficient differs from the original statistic often quoted by economists. In a typical context, the Gini Coefficient would range between 0 and 1\. In the case of portfolio management, we wish to compare a return stream to its cumulative distribution. While the mathematics of the Gini are beyond the scope of this article, the calculation is analogous to a measurement of absolute error that is more complex. In general terms, the absolute error is a measure of dispersion that calculates the average absolute difference of return values from their mean. In contrast, the standard deviation calculates squared errors. This makes the Gini more resistant to the outliers that plague the variance-covariance matrix estimation in a Mean-Variance setting.