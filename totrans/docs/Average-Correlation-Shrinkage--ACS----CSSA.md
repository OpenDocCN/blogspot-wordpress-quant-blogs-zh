<!--yml
category: 未分类
date: 2024-05-12 17:56:56
-->

# Average Correlation Shrinkage (ACS) | CSSA

> 来源：[https://cssanalytics.wordpress.com/2013/10/27/average-correlation-shrinkage-acs/#0001-01-01](https://cssanalytics.wordpress.com/2013/10/27/average-correlation-shrinkage-acs/#0001-01-01)

In the last post on [Adaptive Shrinkage](https://cssanalytics.wordpress.com/2013/10/24/adaptive-shrinkage/ "Adaptive Shrinkage"), the Average Correlation Shrinkage (ACS) model was introduced and compared with other standard shrinkage models.  A spreadsheet demonstrating how to implement ACS can be found here: [average correlation shrinkage](https://cssanalytics.files.wordpress.com/2013/10/average-correlation-shrinkage.xlsx).  This method is meant to be an alternative shrinkage model that can be blended or used in place of standard models. One of the most popular models is the “Constant Correlation Model” which assumes that there is a constant correlation between assets. The strength of this model is that it is a very simple and well-structured estimator. The weakness is that it is too rigid and its performance is dependent on the number of similarly correlated versus uncorrelated assets in the universe. Average Correlation Shrinkage proposes that a good estimator for an asset’s pairwise correlation is the average of all of its pairwise correlations to other assets.  For any pair of assets, their new pairwise correlation is the average of their respective average correlations to all other assets. This makes intuitive sense, and the average is less sensitive to errors than a single correlation estimate. It is also less restrictive than assuming that all correlations are the same.

The graphic below depicts the sample versus the average correlation matrix:

[![average correlation shrinkage](img/352b300dc6d50b37523cd5c9e04912a8.png)](https://cssanalytics.files.wordpress.com/2013/10/average-correlation-shrinkage.png)

As you can see, the average correlation matrix tends to pull down the correlations of the assets that have high correlations, and increases the correlations of the assets that have low correlations.  One can weight the average correlation matrix with the previous sample correlation matrix in some proportion using the following formula:

**adjusted correlation matrix**=w*(average correlation matrix)+(1-w)*sample correlation matrix

By using this shrinkage method to adjust the correlation inputs for optimization, the resulting weights are less extreme towards the assets with a low correlation and assets with a high correlation have a better chance of being included in the final portfolio. Like all shrinkage methods, this is meant to be a sort of compromise

Here is a graphic depicting the final adjusted correlation matrix using a shrinkage factor ![(w)](img/b26a9cd9652d6f591c6ea7df09c0d8cf.png) of .5:

[![adjusted correlation matrix](img/bef820b177ab263cc766dd00e2f270c3.png)](https://cssanalytics.files.wordpress.com/2013/10/adjusted-correlation-matrix.png)