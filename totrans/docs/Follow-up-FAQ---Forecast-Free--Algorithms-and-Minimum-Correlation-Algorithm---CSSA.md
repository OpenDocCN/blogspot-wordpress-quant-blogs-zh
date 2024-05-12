<!--yml
category: 未分类
date: 2024-05-12 18:08:24
-->

# Follow up FAQ: “Forecast-Free” Algorithms and Minimum Correlation Algorithm | CSSA

> 来源：[https://cssanalytics.wordpress.com/2011/08/15/follow-up-faq-forecast-free-algorithms-and-minimum-correlation-algorithm/#0001-01-01](https://cssanalytics.wordpress.com/2011/08/15/follow-up-faq-forecast-free-algorithms-and-minimum-correlation-algorithm/#0001-01-01)

With so many comments and questions regarding the last post [https://cssanalytics.wordpress.com/2011/08/09/forecast-free-algorithms-a-new-benchmark-for-tactical-strategies/](https://cssanalytics.wordpress.com/2011/08/09/forecast-free-algorithms-a-new-benchmark-for-tactical-strategies/) , I decided to take the unusual but more functional approach of writing a FAQ to address these issues for both those that were kind enough to  make intelligent contributions and to new readers. Note that it was brought to my attention that fellow blogger Quantivity has written an excellent series of posts on a similar topic: [http://quantivity.wordpress.com/2011/04/10/portfolio-theory-is-dead-now-what/](http://quantivity.wordpress.com/2011/04/10/portfolio-theory-is-dead-now-what/)

***What is a “Forecast-Free” Algorithm?***

I should have clarified as this is somewhat of a misnomer. Strom Macro [http://strommacro.wordpress.com/](http://strommacro.wordpress.com/)  posted some comments regarding this issue on a recent blog. “Forecast-Free”  in CSS parlance refers to an approach that does not estimate expected returns. In a portfolio algorithm context, this means that we do not care about either relative or absolute conclusions drawn about how an asset class (or stock) should perform. *This does not mean that we do not estimate either correlations or volatility—in fact these estimations are critical to the algorithm*. Estimation error has been shown to be much lower for correlations and volatility than it is for return inputs.  This is why financial engineers spend so much time on the latter rather than the former ( engineers are generally more interested in the most predictable components of time series).

2) ***How is the algorithm constructed?***

At this point, I should mention that I am in the process of compiling a white paper on this topic (forthcoming). The Minimum Correlation Portfolio (MCP) will be the topic of this article, and the benchmark construction will be laid out in complete detail. It uses a more conventional optimization/iterative approach with some interesting twists. In contrast the Minimum Correlation Algorithm (MCA) is an algorithm— it is a heuristic/computational solution designed to be faster and more robust, but is also proprietary. That said, the MCP performance is very close to MCA, and both are based on the same concept.

3) ***Is the algorithm highly sensitive to the choice of asset classes or markets?***

No. This is what differentiates a “forecast-free” approach– both the choice of markets and parameter lengths show substantially less variability than classic “GTAA” approaches. This is because: a) they produce less concentrated portfolios with less correlated constituents b) volatility and correlations can be extrapolated well from almost any time frame, while trends in prices or returns or relative returns/ranks tend to perform best at longer intervals. So while relative strength/momentum and trend-following are robust approaches, I would argue that  “forecast-free” algorithms are even more robust.

4) ***Is the Minimum Correlation Algorithm a variant of risk-parity?***

No. A risk-parity approach assumes equal risk contributions to portfolio risk, it is a hybrid between a minimum variance approach and an equal weight approach. The MCA seeks to optimize risk contributions to reduce portfolio risk with the view of isolating  risk reduction associated with diversification only. That is the best I will say until it is explained in more detail in the paper.

Thank you for all the excellent comments and feedback– I will be releasing a paper on the topic soon enough.  For those that wish to receive the paper directly when it is completed I will post an email address on the blog where you can request a first copy.