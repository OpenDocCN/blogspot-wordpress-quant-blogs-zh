<!--yml
category: 未分类
date: 2024-05-12 18:06:42
-->

# Z-Rank Beta: Identifying Outliers With A Simple Calculation | CSSA

> 来源：[https://cssanalytics.wordpress.com/2012/02/26/z-rank-beta-identifying-outliers-with-a-simple-calculation/#0001-01-01](https://cssanalytics.wordpress.com/2012/02/26/z-rank-beta-identifying-outliers-with-a-simple-calculation/#0001-01-01)

Most conventional quantitative methods from forecasting to optimization suffer from the existence of large outliers in the data. There are many responses to remedy this problem, from using bootstrap/re-sampling techniques to winsorization. In either case these solutions are either computationally intensive or somewhat arbitrary in nature. Sampling intensive procedures are slow and cumbersome, while many winsorization procedures entail cropping the the data to compute trimmed means or replacing observations at the extremes with the 95th/5th values. More extensive winsorization techniques are also computationally intensive.

In general outliers can hurt both the bias (accuracy of actual versus predicted) and the variance (sensitivity to the sample data) of the predictor. The bias/variance tradeoff is analogous to trying to find the best model without over-fitting the sample data. Outliers cause a change in both the nature of the model selected and also the responsiveness of the variance of the model to a more normal sample. As a consequence, outliers need to be dealt with to avoid mis-specification. Once the outliers can be identified and influence of these outliers are reduced, it is possible to construct a better model of the data. In finance, volatility, correlations, covariances and other measures are already being applied to noisy time-series data and it is even more important to address these issues.

There is a simple calculation I would like to call the “Z-Rank Beta” that looks at the relationship between the normalized data and a cumulative distribution. Essentially this is the slope of the probability distribution (z-score of a normal distribution converted to a probability) of input values and the percentile ranking of input values. The difference between the two measures is that the z-score is not bounded and symmetric, while the percentile ranking is always bounded and symmetric. Thus to the extent the z-score differs substantially from the percentile ranking, the beta will be considerably lower than 1, while a perfect match would generally be closer to 1\. The best way to test the statistic is to run a regression to derive the beta and use the p-value to identify whether the deviation is significant. To compute the Z-Rank Beta the calculation would be:

1) Use an array of at least 20 values
2) Find the percentile ranking of each value in the array
3) Compute the z-score of each value in the array: (x-average(x1,x2…))/stdeva(x1,x2…)
4) Convert the z-scores to probabilities–in excel: NORMSDIST(z1,z2….)
5) Compute the Z-Rank Beta as:
covariance(percentile rankings,probabilities)/variance(percentile rankings)

As a general guideline, beta values less than .95 indicate the possible presence of an outlier (or more than one), and values below .9 show a definite mismatch. Using a regression is superior to be able to test the significance and also identify the specific residuals that are the largest.