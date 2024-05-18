<!--yml
category: 未分类
date: 2024-05-18 14:00:47
-->

# S&P 500 Sectors Analysis – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2011/01/29/sp-500-sectors-analysis/#0001-01-01](https://quantumfinancier.wordpress.com/2011/01/29/sp-500-sectors-analysis/#0001-01-01)

To follow up with last post, and also nicely tying into Engineering Returns’ recent sector [rotational system](http://engineering-returns.com/2011/01/28/spy-usage-of-adaptive-sector-rotation-model-to-improve-returns/) I will show a factor decomposition of the S&P 500 from different sectors. In essence, you can think of it as a multifactor analysis where I try to determine what sectors are relevant for a given period in predicting the S&P 500\. This kind of analysis is important since a lot of the point and click trading in proprietary firms is done based of price action and correlation across markets. It is the later part I address today.

I looked at the period going from Jan. 01 2008 to today in both analyses. When using linear least squares we perform the regression on the next day SPY returns using the current return of our sector ETFs (I used the SPDRs) as independent variables. Results are below:

[![](img/a095319172c27beec9c0d020a7d7104d.png "spsectorols")](https://quantumfinancier.wordpress.com/wp-content/uploads/2011/01/spsectorols.png)

What we see from the table is that the consumer discretionary, financials, materials and technology sectors have statistically significant. Additionally, the financials and technology sectors seem to be precursors of reversals as indicated by their negative coefficients. The opposite holds true with the consumer discretionary and materials sector who seem to not be so contrarian. This simple analysis seems to indicate that these four sectors are the best candidates to consider when looking into cross markets relationships.

Another aspect of trading where factor analysis can come into play is related to diversification benefits. Using principal component analysis we extract the co-movements of our sector ETFs and SPY. Similarly, we could use the same type of method to extract the co-movements across country indices, or some other discretionary breakdown. Looking at the factor loading for the first three (explain about 95% of the covariance matrix) principal components for each ETF, we can get a better feel of the value of allocating capital to an ETF versus another and puts the illusion of diversification in perspective. In our days where correlation across asset classes is high, people trading TAA systems have all the advantages to use such analysis in their asset allocation and weighting. The factor loadings are below:

[![](img/643588e097be14edaa11e66ccf4d6784.png "spsectorfactors")](https://quantumfinancier.wordpress.com/wp-content/uploads/2011/01/spsectorfactors.png)

Meric et al. (2006) say it best: “The sectors with high factor loadings in the same principal component move closely together making them poor candidates for diversification benefits. The higher the factor loading of a sector in a principal component, the higher its correlation is with the other sectors with high factor loadings in the same principal component. The sector indexes with high factor loadings in different principal components do not move closely together and they can provide greater diversification benefit. Some sector indexes may have high factor loadings in more than one principal component. It indicates that the movements of these sectors have some similarity to the movements of sectors with high factor loadings in more than one principal component. These sectors are not good prospects for successful sector portfolio diversification.” In depth interpretation of the table is left to the curious reader.

In conclusion, factor decomposition/analysis can be very useful for traders to get a feel of their traded instrument of predilection. Be it for establishing significant lead/lag relationship or diversification caveats, both least squares and PCA can be valuable tools. Interested readers can also look at Granger causality for similar avenues.

QF