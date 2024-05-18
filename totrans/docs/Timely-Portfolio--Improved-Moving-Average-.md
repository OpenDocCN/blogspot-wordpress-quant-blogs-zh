<!--yml
category: 未分类
date: 2024-05-18 15:10:13
-->

# Timely Portfolio: Improved Moving Average?

> 来源：[http://timelyportfolio.blogspot.com/2011/12/improved-moving-average.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/12/improved-moving-average.html#0001-01-01)

*I have been notified by the authors that the code does not perfectly reflect the improved moving average introduced.  In another post, I will explore the differences.  The authors have now released their version of the code [http://www.quantf.com/fotis-papailias/improved-moving-average-code-is-available-for-download/332](http://www.quantf.com/fotis-papailias/improved-moving-average-code-is-available-for-download/332 "http://www.quantf.com/fotis-papailias/improved-moving-average-code-is-available-for-download/332").*

When [@quantfblog](http://twitter.com/#!/quantfblog) started following me on Twitter, I was delighted to discover their papers

> [Papailias, Fotis and Thomakos, Dimitrios D., An Improved Moving Average Technical Trading Rule (September 11, 2011). Available at SSRN: http://ssrn.com/abstract=1926376](http://ssrn.com/abstract=1926376)
> 
> [Papailias, Fotis and Thomakos, Dimitrios D., An Improved Moving Average Technical Trading Rule II - Can We Obtain Performance Improvements with Short Sales? (November 12, 2011). Available at SSRN: http://ssrn.com/abstract=1958906](http://ssrn.com/abstract=1958906)

backed by a nice and improving website [http://www.quantf.com](http://www.quantf.com).  I just could not resist the opportunity to port their improved moving average idea to R and run some additional tests.  The entire process was extremely pleasant due to the authors’ willingness to test, comment, and suggest throughout the implementation process.  Thanks so much to them for all their help.

In this process, I AM NOT OFFERING INVESTMENT ADVICE.  THIS IS SIMPLY A TEST/ILLUSTRATION.  PURSUING THESE CONCEPTS WILL MOST LIKELY LOSE SIGNIFICANT AMOUNTS (ALL) OF YOUR MONEY.

For fun, I thought it would be interesting to compare the "Improved Moving Average" to a [Mebane Faber](http://mebanefaber.com) style 10-month moving average system.

While I enjoyed the testing, I am still not entirely sure if the “improved moving average” is significantly improved, but it certainly might fit someone’s utility curve better than the standard moving average.  More than anything, this process has proven to me a couple of things:

> 1) the beauty of open-source and collaboration.  The authors were incredibly generous and helpful as I worked through this process.  To even better demonstrate the power of open-source, I will use ttrTests to do additional testing and then the bt examples from [http://systematicinvestor.wordpress.com](http://systematicinvestor.wordpress.com) in future posts.
> 
> 2) how even a simple moving average can become incredibly complex.  Making one very slight change markedly changes the results.

[R code from GIST:](https://gist.github.com/1405561)