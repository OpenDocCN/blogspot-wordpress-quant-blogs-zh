<!--yml
category: 未分类
date: 2024-05-12 17:57:03
-->

# Adaptive Shrinkage | CSSA

> 来源：[https://cssanalytics.wordpress.com/2013/10/24/adaptive-shrinkage/#0001-01-01](https://cssanalytics.wordpress.com/2013/10/24/adaptive-shrinkage/#0001-01-01)

The covariance matrix can be quite tricky to model accurately due to the [curse of dimensionality](https://cssanalytics.wordpress.com/2013/10/06/random-subspace-optimization-rso/ "Random Subspace Optimization (RSO)"). One approach to improving estimation is to use “shrinkage” to a well-structured estimator. The general idea is that a compromise between a logical/theoretical estimator and a sample estimator will yield better results than either method. It is analogous to saying that in the summer, the temperature in many states is likely to be 80 degrees and that you will blend your weather forecast estimate with this baseline number in some proportion to reduce forecast error.

Here are two good articles worth reading as a primer:

[honey i shrunk the sample covariance matrix](https://cssanalytics.files.wordpress.com/2013/10/honey-i-shrunk-the-sample-covariance-matrix.pdf)– Ledoit/Wolf

[shrinkage-simpler is better](https://cssanalytics.files.wordpress.com/2013/10/shrinkage-simpler-is-better.pdf)  – Benninga

Michael Kapler of [Systematic Investor](http://systematicinvestor.wordpress.com/) and I tested a wide variety of different shrinkage approaches at the beginning of the year on numerous datasets. Michael is perhaps the most talented and experienced person I have ever worked with (both from a quant and also from a programming standpoint), and it is always a pleasure to get his input. Two interesting ideas evolved from the research: 1) Average Correlation Shrinkage Model (ACS): the correlation between each asset versus all other assets as used in the [Minimum Correlation Algorithm](https://cssanalytics.wordpress.com/2012/09/27/minimum-correlation-implementation-in-excel/ "Minimum Correlation: Implementation in Excel") is a logical shrinkage model that produces very competitive performance and is simpler to implement that most other models (spreadsheet to follow in the next post) 2) Adaptive Shrinkage:  this chooses the “best” model from a number of different shrinkage models based on the version that delivered the best historical sharpe ratio for minimum variance allocation.

Adaptive Shrinkage makes a lot of sense since the appropriate shrinkage estimator to use is different depending on the composition of the asset universe. For example a universe with one bond and fifty stocks will perform better with a different shrinkage estimator than one with all stocks or multiple diverse asset classes.  In addition, there may be one model that is a composite of different estimators for example, that consistently performs better than others.  In our testing, we chose to define success as the out-of-sample sharpe ratio attained by minimizing variance using a given estimator. This makes more sense than minimizing volatility- which is often used in the literature to evaluate different shrinkage approaches. A higher sharpe ratio  implies that you could achieve lower volatility than a sample minimum variance (assuming volatility happens to be higher) by holding some proportion of your portfolio in cash.  However, the objective function for Adaptive Shrinkage could be anything that you would like to achieve—for example minimum turnover might also be an objective, or some combination of minimum turnover with maximum sharpe ratio.  Here are some of the different shrinkage estimators that we tested. Note that “Average David” refers to the ACS/Average Correlation Shrinkage:

**S = sample covariance matrix (no shrinkage)
* A50= 50% average.david + 50% sample**

*** S_SA_A= 1/3*[average + sample + sample.anchored] **

*** A_S= average.david and sample using Ledoit and Wolf math
* D_S= diagonal and sample using Ledoit and Wolf math
* CC_S=constant correlation and sample using Ledoit and Wolf math
* SI_S= single index  and sample using Ledoit and Wolf math
* SI2_S=two.parameter covariance matrix  and sample using Ledoit and Wolf math
* AVG_S= average and sample using Ledoit and Wolf math, where average = 1/5 * (average.david + diagonal + constant correlation + single index + two.parameter covariance matrix)**

*** A= average.david
* D= diagonal
* CC=constant correlation
* SI= single index
* SI2=two.parameter covariance matrix
* AVG= average = 1/5 * (average.david + diagonal + constant correlation + single index + two.parameter covariance matrix)**

* **Best Sharpe=Adaptive Shrinkage -invest all capital into the method (S or SA or A) that has the best sharpe ratio over the last 252 days**

We used a 60-day parameter to compute the variance/covariance matrix, and 252 days as a lookback to find the shrinkage method with the best sharpe ratio. The report/results can be found here: [all60 comprehensive](https://cssanalytics.files.wordpress.com/2013/10/all60-comprehensive.pdf). Interestingly enough the Adaptive Shrinkage/Best Sharpe produced the highest sharpe ratio on almost all datasets. This demonstrates a promising method to potentially improve upon a standard shrinkage approach, and also remove the need to determine which is the best model to use as the base estimator. Readers can draw their own conclusions from the results from this extensive report. I would generalize by saying that most shrinkage estimators produce similar performance, and that combinations of estimators seem to perform better than single estimators. Shrinkage does not deliver substantial improvements in performance versus just using the sample estimator in these tests. Finally, the Average Correlation Shrinkage Model is very competitive if not superior to most estimators and it delivers lower turnover as well. This is true of many of the different variants that use the ACS.