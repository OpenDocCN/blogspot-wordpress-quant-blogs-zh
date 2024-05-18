<!--yml
category: 未分类
date: 2024-05-18 15:11:48
-->

# Timely Portfolio: ttrTests: Its Great Thesis and Incredible Potential

> 来源：[http://timelyportfolio.blogspot.com/2011/09/ttrtests-its-great-thesis-and.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/09/ttrtests-its-great-thesis-and.html#0001-01-01)

I stumbled on the ttrTests R package as mentioned in my post [ttrTests Experimentation](http://timelyportfolio.blogspot.com/2011/08/ttrtests-experimentation.html).  I did not recognize its potential until I spent much more time absorbing the basis of the package—David St. John’s thesis [Technical Analysis Based on Moving Average Convergence and Divergence](http://math.uic.edu/~dstjohn/thesis.pdf).  Since the title specifically addresses MACD, which I have had little luck implementing, I dismissed much of the content.  However, the power of the thesis extends well beyond MACD to all systematic methods and describes tests to ensure luck is not the source of a system’s returns.  In the package documentation, there is a summary of the 5 main tests:

> “Contains five major tests supported by other functions: Did the TTR strategy outperform a benchmark in the past data? Is the excess return significant, using bootstrapping to construct a confidence interval? Is the excess return explained by data snooping? Is the ’good’ choice of parameters robust across sub-samples? Is this robustness significant, using bootstrapping to construct a confidence interval?”

The tests expose luck, data snooping, trading costs, and parameter persistence across both degrees of freedom and subperiods.  I look forward to documenting its power in my blog and also potentially working with the author to include in other R packages such as quantstrat.

Since I am running out of time, I first want to apply each of the tests to MACD in the same style as the package documentation and the thesis paper, but this time on a xts DJI object gathered through getSymbols rather than the spData provided with the package.

The output from the tests is very cumbersome, but I hope this set of examples will help provide a flavor for the package and its powerful tests.  In my next couple of posts, I will run each test in much further detail on my basic custom CUD indicator and try to get the cumbersome output in a far more digestible and graphical format.

[R code (click to download from Google Docs):](https://docs.google.com/leaf?id=0B2qp2r96khJPMDZjNjA3M2UtNDI2OS00NTRjLTg3ZjgtNzVlY2MxZDEzMmUz&hl=en_US)

```
require(ttrTests)
require(quantmod)   #get Dow Jones Industrials from Yahoo! Finance
getSymbols("^DJI",from="1896-01-01",to=Sys.Date())
#convert closing price to vector format which works best with ttrTests
DJI.vector <- as.vector(DJI[,4])   #using the defaults as mentioned in the thesis paper on MACD
#show each of the tests in order of their mention   #quotes are from ttrTests package documentation
#"compares the performance of the TTR with some benchmark"
returnStats(DJI.vector)   #"constructs a confidence interval for this performance"
#"and gives a p-value for the excess return observed in (1)."
nullModel(DJI.vector)   #"constructs a p-value for the ’best’ choice"
#"of parameters within a given domain"
dataSnoop(DJI.vector,bSamples=3,test="RC")
dataSnoop(DJI.vector,bSamples=3,test="SPA")   #"asks whether or not good choices of parameters"
#"were robust across different time periods"
#chose 8 since data is from 1928 will approximate by decade
subperiods(DJI.vector, periods=8)   #and my favorite of all
#"tests if the persistence measure from subperiods()"
#"is statistically significant"
#this takes the longest (about 10 minutes on my i7 laptop)
paramPersist(DJI.vector)
```

[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")