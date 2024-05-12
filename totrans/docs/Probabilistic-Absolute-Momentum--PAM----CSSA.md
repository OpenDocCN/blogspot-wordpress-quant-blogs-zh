<!--yml
category: 未分类
date: 2024-05-12 17:55:01
-->

# Probabilistic Absolute Momentum (PAM) | CSSA

> 来源：[https://cssanalytics.wordpress.com/2014/03/03/probabilistic-absolute-momentum-pam/#0001-01-01](https://cssanalytics.wordpress.com/2014/03/03/probabilistic-absolute-momentum-pam/#0001-01-01)

In the last post on [Probabilistic Momentum](https://cssanalytics.wordpress.com/2014/01/28/are-simple-momentum-strategies-too-dumb-introducing-probabilistic-momentum/ "Are Simple Momentum Strategies Too Dumb? Introducing Probabilistic Momentum") we introduced a simple method to transform a standard momentum strategy to a  probability distribution to create confidence thresholds for trading. The spreadsheet used to replicate this method can be found [here](https://cssanalytics.wordpress.com/2014/02/12/spreadsheet-correction-probabilistic-momentum/ "Spreadsheet Correction- Probabilistic Momentum"). This framework is intellectually superior to a binary comparison  between two assets because the tracking error of choosing one versus the other is not symmetric across momentum opportunities. The opportunity cost of choosing one asset versus another is embedded in this framework, and using a confidence threshold that is greater than 50% will help to standardize the risk of momentum decisions across diffferent pairings (for example using momentum with stocks and bonds is more risky than with say the S&P500 and the Nasdaq).

The same concept can be used for creating an absolute momentum methodology–this concept was introduced by Gary Antonacci of [Optimal Momentum](http://optimalmomentum.blogspot.com/) in a paper [here](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=2042750). The general idea for those that are not familiar, is that you can use the relative momentum between a target asset-say equities- and some low-risk asset such as t-bills or short-term treasurys (cash) to generate switching decisions between the target and cash. This can be used instead of applying a simple moving average strategy to the underlying asset. In this case we can apply the same approach with Probabilistic Momentum with a short-term treasury ETF such as SHY with some target asset to create a Probabilistic Absolute Momentum strategy (PAM). In this case, I created an example with the Nasdaq (QQQ) and 1-3 year treasurys (SHY) and used the maximum period of time when both had history available (roughly 2800 bars).  I chose 60% as the confidence threshold to switch between QQQ and SHY. The momentum lookback window chosen was 120-days. We did not assume any trading costs in this case–but that would favor PAM even more. Here is a chart of the historical transitions of using the probabilistic approach (PAM) versus a simple absolute momentum approach:

[![PAM 1](img/f68c0cf9375e3e87ebe19723d67c7683.png)](https://cssanalytics.files.wordpress.com/2014/03/pam-1.png)

Here is the performance breakdown of applying this strategy:

[![PAM2](img/abe95e2f924a27939b932ca0475d8856.png)](https://cssanalytics.files.wordpress.com/2014/03/pam2.png)

Here we see that Probabilistic Absolute Momentum reduces the number of trades by over 80% from 121 to 23\. The raw performance is improved by almost 2%, and the sharpe ratio is improved by roughly 15%.  More importantly, from a psychological standpoint using PAM is much easier to use and stick with as a discretionary trader or even as a quantitative portfolio manager. It eliminates a lot of the costly whipsaws that result from trying to switch between being invested and being in cash.  It also makes it easier to overlay an absolute momentum strategy on a standard momentum strategy since there is less interference from the cash decision.