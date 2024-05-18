<!--yml
category: 未分类
date: 2024-05-18 15:34:06
-->

# Network Model | Tr8dr

> 来源：[https://tr8dr.wordpress.com/2010/02/16/network-model/#0001-01-01](https://tr8dr.wordpress.com/2010/02/16/network-model/#0001-01-01)

February 16, 2010 · 11:46 pm

I’ve been thinking about the relationships amongst a network of assets.   Supposing I have a network of hundreds of assets, what sort of measurements can be made that allow for statements about the future state with a measurable degree of confidence.

[![](img/ce338b6eaa23df2e74a8527f0c67f038.png "group1")](https://tr8dr.wordpress.com/wp-content/uploads/2010/01/group1.png)

Here are some “standard” approaches to looking at the relationship between assets:

1.  **Covariance**
    Covariance is a linear measure, the normalization of which is literally the slope of a least-squares regression line through paired data.  Has issues with lagged series and assumes linearity, also only uniquely specifies elliptical distributions.
2.  **Cointegration
    Cointegration is a measure of relationship between series using an autoregressive error correction model.   It avoids many of the issues of Covariance, however, like covariance is not sufficient to uniquely specify the joint distribution.   The VECM model and Johansen method give robust estimates of this.** 
3.  **Distribution Estimating Models**
    Models that estimate the distribution (i.e. provide the most probable price movement in the next sample period based on an estimated high-dimensional distribution); works well on certain portfolios.
4.  **SDEs
    SDEs that impose a structure / mechanism of price movement, implying future price movements.   These models often combine points 1 and 3\.   I like most other people in this space have a collection of these, some better than others.**

Given that I already have models in categories 3 and 4,  am interested in a new model based on cointegration — not cointegration for pairs trading, but using the strong error-correcting relationships in a network of assets to determine likely next period moves.

Amongst a number of approaches for determining error-correcting relationships, have found the eigenvectors implied by the Johansen maximum likelihood estimate of the VECM to be the most stable as compared to other alternatives:

1.  heuristic zero crossings maximization
2.  beta estimates from rolling OLS regressor
3.  Various Ornstein-Uhlenbeck models (though with a particle filter the degree of noise can be reduced significantly)

I’m not going to state what I am doing right now, but may write up parts of it along the way.