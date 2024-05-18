<!--yml
category: 未分类
date: 2024-05-18 14:42:05
-->

# Multiple Factor Model Summary | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2012/03/11/multiple-factor-model-summary/#0001-01-01](https://systematicinvestor.wordpress.com/2012/03/11/multiple-factor-model-summary/#0001-01-01)

[Home](https://systematicinvestor.wordpress.com/ "Go to homepage")

>

[Factor Model](https://systematicinvestor.wordpress.com/category/factor-model/)

,

[Factors](https://systematicinvestor.wordpress.com/category/factors/)

> Multiple Factor Model Summary

## Multiple Factor Model Summary

In this post I want to summarize all the material I covered in the Multiple Factor Models series. The [Multiple Factor Model](http://www.investopedia.com/terms/m/multifactor-model.asp) can be used to decompose returns and calculate risk. Following are some examples of the Multiple Factor Models:

The factors in the model are usually created using pricing, fundamental, analyst estimates, and proprietary data. I will only show examples of factors using pricing and fundamental data because these infromation is readily available from Yahoo Fiance and ADVFN.

Following is a summary of all posts that I wrote about Multiple Factor Models:

1.  [Multiple Factor Model – Fundamental Data](https://systematicinvestor.wordpress.com/2012/01/29/multiple-factor-model-fundamental-data/) – in this post I demonstrate how to get company’s Fundamental Data into R, create a simple factor, and run correlation analysis.
2.  [Multiple Factor Model – Building Fundamental Factors](https://systematicinvestor.wordpress.com/2012/02/04/multiple-factor-model-building-fundamental-factors/) – in this post I demonstrate how to build Fundamental factors described in the CSFB Alpha Factor Framework and compute quantiles spreads. For details of the CSFB Alpha Factor Framework please read [CSFB Quantitative Research, Alpha Factor Framework on page 11, page 49 by P. N. Patel, S. Yao, R. Carlson, A. Banerji, J. Handelman](http://www.scribd.com/mobile/documents/62210581/download?commit=Download+Now&secret_password=).
3.  [Multiple Factor Model – Building CSFB Factors](https://systematicinvestor.wordpress.com/2012/02/13/multiple-factor-model-building-csfb-factors/) – in this post I demonstrate how to build majority of factors described in the CSFB Alpha Factor Framework, run cross sectional regression to estimate factor loading, create and test Alpha model.
4.  [Multiple Factor Model – Building Risk Model](https://systematicinvestor.wordpress.com/2012/02/21/multiple-factor-model-building-risk-model/) – in this post I demonstrate how to build a multiple factor risk model, compute factor covariance using shrinkage estimator, forecast stocks specific variances using GARCH(1,1).
5.  [Portfolio Optimization – Why do we need a Risk Model](https://systematicinvestor.wordpress.com/2012/02/26/portfolio-optimization-why-do-we-need-a-risk-model/) – in this post I explain why do we need a risk model and demonstrate how it is used during portfolio construction process.
6.  [Multiple Factor Model – Building 130/30 Index](https://systematicinvestor.wordpress.com/2012/03/06/multiple-factor-model-building-13030-index/) – in this post I demonstrate how to build 130/30 Index based on the CSFB Factors and the Risk Model we created previously. The [130/30: The New Long-Only (2008) by A. Lo, P. Patel](http://math.nyu.edu/faculty/avellane/Lo13030.pdf) paper presents a very detailed step by step guide to building 130/30 Index using average CSFB Factors as the alpha model and [MSCI Barra Multi-Factor Risk model](http://www.alacra.com/alacra/help/barra_handbook_US.pdf).
7.  [Multiple Factor Model – Building 130/30 Index (Update)](https://systematicinvestor.wordpress.com/2012/03/10/multiple-factor-model-building-13030-index-update/) – in this post I demonstrate how to build Market-Neutral and Minimum Variance strategies and compare their performance to the 130/30 Index.

There is an excellent discussion of portfolio construction problems and possible solutions in the [The top 7 portfolio optimization problems](http://www.portfolioprobe.com/2012/01/05/the-top-7-portfolio-optimization-problems/) post by Pat Burns. I want to highlight two problems that are relevant to the Multiple Factor Models.