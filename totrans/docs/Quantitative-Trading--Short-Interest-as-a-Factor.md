<!--yml
category: 未分类
date: 2024-05-12 18:58:56
-->

# Quantitative Trading: Short Interest as a Factor

> 来源：[http://epchan.blogspot.com/2014/05/short-interest-as-factor.html#0001-01-01](http://epchan.blogspot.com/2014/05/short-interest-as-factor.html#0001-01-01)

Readers of zerohedge.com will no doubt be impressed by this

[chart](http://www.zerohedge.com/sites/default/files/images/user5/imageroot/2014/02/20140221_SI.png)

 and the accompanying

[article](http://www.zerohedge.com/news/presenting-most-shorted-stocks)

:

| ![](img/ddba574b72fa31c8d87f727d17a8fd0c.png "Cumulative returns of most shorted stocks relative to SPX") |
| Cumulative Returns of Most Shorted Stocks in 2013 |

Indeed, short interest (expressed as the number of shares shorted divided by the total number of shares outstanding) has long been thought to be a useful factor. To me, the counter-intuitive wisdom is that the more a stock is shorted, the better is its performance. You might explain that by saying this is a result of the "short squeeze", when there is jump in price perhaps due to news and stock lenders are eager to sell the stock they own. If you have borrowed this stock to short, your borrowed stock may be recalled and you will be forced to buy cover at this most inopportune time. But this is an unsatisfactory explanation, as this will result only in a short term (upward) momentum in price, not the sustained out-performance of the most shorted stocks. This long-term out-performance seems to suggest that short sellers are less informed than the average trader, which is odd.

Whatever the explanation, I am intrigued to find out if short interest really is a good factor to incorporate into a comprehensive factor model over the long term.

The result? Not particularly impressive. It turns out that 2013 was one of the best years for this factor (hence the impressive chart above). For that year, a daily-rebalanced long-short portfolio (long 50 most shorted stocks and short 50 least shorted stocks in the SPX) returned 6.9%, with a Sharpe ratio of 2 and a Calmar ratio of 2.9\. However, if we extend our backtest to 2007, the APR is only 2.8%, with a Sharpe ratio of 0.5 and a Calmar ratio of 0.3\. This backtest was done using survivorship-bias-free data from CRSP, with short interest data provided by Compustat.

Here is the cumulative returns chart from 2007-2013:

| [![](img/65583be8a69752776f9c4c166568659d.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiIJmlqWSyqTgIFkI2pzKLdW-eV2iPEtQx9y3IX6morpJ0U6OYl-SXMzdwrxdmqNnSBQtkN-g5YwYcSbz-o0AOtOb02YIDd-C4Zhsiodm8TQ2bnK6kIV8F6zxtuhZGsRrw55qABPA/s1600/Cumulative+Returns+of+Short+Interest+Factors+2007+to+2013.png) |
| Cumulative Returns of LS Portfolio based on Short Interest: 2007-2013 |

Interesting, trying this on the SP600 small-cap universe yielded negative returns, possibly meaning that short-sellers of small caps do have superior information.

I promise, this will be the last time I talk about factors in a while!

===

**Tech Update:**

I was shocked to learn that Matlab now offers licenses for just $149 - the so-called 

[Matlab Home](http://www.mathworks.com/products/matlab-home/)

  (h/t: Ken H.) In addition, its Trading Toolbox now offers API connection to Interactive Brokers, in addition to a few other brokerages. I am familiar with both Matlab and R, and while I am impressed by the large number of free, sophisticated statistical packages in R, I still stand by Matlab as the most productive platform for developing our own strategies. The Matlab development (debugging) environment is just that much more polished and easy-to-use. The difference is bigger than Microsoft Word vs. Google Docs.

A reader Ravi B. told me that there is a website called www.seasonalgo.com if you want to try out different seasonal futures strategies.

Finally, a startup at

[inovancetech.com](http://inovancetech.com/)

 offers machine learning algorithms to help you find the best combination of technical indicators for trading FX.

===

**Workshops Update:**

I am now offering the

*Millisecond Frequency Trading*

(MFT) Workshop as an online course on June 26- 27\. Previously, I have only offered it live in London and to a few institutional investors. It has two main parts:

Part 1: introducing techniques for traders who want to

*avoid*

HFT predators.

Part 2: how to backtest a strategy that requires tick data with millisecond resolution using Matlab.

The example strategy used is based on order flow. For more details, please visit

[epchan.com/my-workshops](http://epchan.com/my-workshops)

.

Additionally, I will be teaching the Mean Reversion and Momentum (but not MFT) workshops in Hong Kong on June 17-20.