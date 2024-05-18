<!--yml
category: 未分类
date: 2024-05-18 13:43:45
-->

# Why Log Returns | Quantivity

> 来源：[https://quantivity.wordpress.com/2011/02/21/why-log-returns/#0001-01-01](https://quantivity.wordpress.com/2011/02/21/why-log-returns/#0001-01-01)

A reader recently asked an important question, one which often puzzles those new to quantitative finance (especially those coming from [technical analysis](http://en.wikipedia.org/wiki/Technical_analysis), which relies upon price pattern analysis):

> Why use the logarithm of returns, rather than price or raw returns?

The answer is several fold, each of whose individual importance varies by problem domain.

Begin by defining a return: ![r_i](img/86041fc7cdb750d937fb4e877af28a1e.png) at time ![i](img/6aed483d693a0743f647c27ec4372c2a.png), where ![p_i](img/cf77e53f898b49e52240e8ba57932b24.png) is the price at time ![i](img/6aed483d693a0743f647c27ec4372c2a.png) and ![j \equiv (i - 1)](img/1aca8f5dfc45306cceb405d34f6622a3.png):

    ![r_i = \frac{p_i - p_j}{ p_j } ](img/49ecbc13c2cb8772895271279f41192a.png)

Benefit of using *returns*, versus prices, is *normalization*: measuring all variables in a comparable metric, thus enabling evaluation of analytic relationships amongst two or more variables despite originating from price series of unequal values. This is a requirement for many multidimensional statistical analysis and machine learning techniques. For example, interpreting an equity [covariance matrix](http://en.wikipedia.org/wiki/Covariance) is made sane when the variables are both measured in percentage.

Several benefits of using *log returns*, both theoretic and algorithmic.

First, *log-normality*: if we *assume* that prices are distributed [log normally](http://en.wikipedia.org/wiki/Log-normal_distribution) (which, in practice, may or may not be true for any given price series), then ![log(1 + r_i)](img/f97d06f6d5c52058818dda135267a3b7.png) is conveniently [normally distributed](http://en.wikipedia.org/wiki/Normal_distribution), because:

    ![1 + r_i = \frac{p_i}{p_j} = \exp^{\log(\frac{p_i}{p_j})} ](img/7e6e5fcd19efb43c4a5e3b84e92ea0c2.png)

This is handy given much of classic statistics presumes normality.

Second, *approximate raw-log equality*: when returns are very small (common for trades with short holding durations), the following approximation ensures they are close in value to raw returns:

    ![\log(1 + r) \approx r](img/3c8ca8caed09f6fd7ed86e7608569b03.png) , ![r \ll 1 ](img/1abb56562a0bb9449d4a6af15e3fe057.png)

Third, *time-additivity*: consider an ordered sequence of ![n](img/4f0c9881324df3a61e8d3cc580ec06e6.png) trades. A statistic frequently calculated from this sequence is the *compounding return*, which is the running return of this sequence of trades over time:

    ![\displaystyle (1 + r_1)(1 + r_2)  \cdots (1 + r_n) = \prod_i (1+r_i)](img/c70af4ee8d1b96751b4118512fe679d3.png)

This formula is fairly unpleasant, as probability theory reminds us the product of normally-distributed variables is *not normal*. Instead, the sum of normally-distributed variables is normal (important technicality: only when all variables are *uncorrelated*), which is useful when we recall the following logarithmic identity:

    ![\log(1 + r_i) = log(\frac{p_i}{p_j}) = \log(p_i) - log(p_j) ](img/ebe0b43bc7b39f463d9699826cc219b6.png)

Thus, compounding returns are normally distributed. Finally, this identity leads us to a pleasant algorithmic benefit; a simple formula for calculating compound returns:

    ![\displaystyle \sum_i \log(1+r_i) = \log(1 + r_1) + \log(1 + r_2)  + \cdots + \log(1 + r_n) = \log(p_n) - \log(p_0)](img/f3f8851ad0094949ddd8d083b0397afc.png)

Thus, the compound return over *n* periods is merely the difference in log between initial and final periods. In terms of [algorithmic complexity](http://en.wikipedia.org/wiki/Big_O_notation), this simplification reduces O(n) multiplications to O(1) additions. This is a huge win for moderate to large *n*. Further, this sum is useful for cases in which returns diverge from normal, as the [central limit theorem](http://en.wikipedia.org/wiki/Central_limit_theorem) reminds us that the sample average of this sum will converge to normality (presuming finite first and second moments).

Fourth, *mathematical ease*: from [calculus](http://en.wikipedia.org/wiki/Calculus), we are reminded (ignoring the [constant of integration](http://en.wikipedia.org/wiki/Constant_of_integration)):

    ![e^x = \int e^x dx = \frac{d}{dx} e^x = e^x ](img/1aec1a820b3d7042a5267a1a05c4ac64.png)

This identity is tremendously useful, as much of financial mathematics is built upon [continuous time stochastic processes](http://en.wikipedia.org/wiki/Continuous-time_stochastic_process) which rely heavily upon integration and differentiation.

Fifth, *numerical stability*: addition of small numbers is numerically safe, while multiplying small numbers is not as it is subject to [arithmetic underflow](http://en.wikipedia.org/wiki/Arithmetic_underflow). For many interesting problems, this is a serious potential problem. To solve this, either the algorithm must be modified to be numerically robust or it can be transformed into a numerically safe summation via logs.

As suggested by John Hall, there are downsides to using log returns. Here are two recent papers to consider (along with their references):