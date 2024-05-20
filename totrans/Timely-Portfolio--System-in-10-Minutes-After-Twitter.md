<!--yml
category: 未分类
date: 2024-05-18 15:11:15
-->

# Timely Portfolio: System in 10 Minutes After Twitter

> 来源：[http://timelyportfolio.blogspot.com/2011/10/system-in-10-minutes-after-twitter.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/10/system-in-10-minutes-after-twitter.html#0001-01-01)

On Twitter last night, I spotted @milktrader from [www.algorithmzoo.com](http://www.algorithmzoo.com) doing some range research on equity indexes.  I offered a tweet on the crazy Russell 2000 17% move over 7 days.  Within 10 minutes, I discovered a signal that worked very well.  It probably is worthless, but I thought I would share in case someone cares to play with it.  THIS IS NOT INVESTMENT ADVICE AND WILL PROBABLY LOSE INCREDIBLE AMOUNTS OF MONEY.  If nothing else, it illustrates the power of R.

R code:

require(quantmod)
require(PerformanceAnalytics)
getSymbols("^RUT",from="1896-01-01",to=Sys.Date())
signal<-ifelse(runMax(RUT[,2],7)/runMin(RUT[,3],7)-1-
    ROC(RUT[,4],n=20,type="discrete")<0.02,1,0)
perf<-merge(lag(signal,k=1)*ROC(RUT[,4],type="discrete",n=1),
    ROC(RUT[,4],type="discrete",n=1))
colnames(perf)<-c("System","Russell 2000")
charts.PerformanceSummary(perf,ylog=TRUE,
    main="Quick Untested Russell 2000 System")