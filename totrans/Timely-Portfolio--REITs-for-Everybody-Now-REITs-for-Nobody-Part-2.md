<!--yml
category: 未分类
date: 2024-05-18 15:14:38
-->

# Timely Portfolio: REITs for Everybody Now REITs for Nobody Part 2

> 来源：[http://timelyportfolio.blogspot.com/2011/06/reits-for-everybody-now-reits-for.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/06/reits-for-everybody-now-reits-for.html#0001-01-01)

As a quick follow-up to my first [REITs for Everybody Might Now Mean REITs for Nobody](http://timelyportfolio.blogspot.com/2011/06/reits-for-everybody-might-now-mean.html), I want to look at REITs and High Yield bonds, which also might simultaneously attract conservative yield buyers and speculative beta chasers.

[HYG (iShares High Yield) and IYR (iShares REIT)](http://stockcharts.com/h-sc/ui?s=hyg&p=w&st=2007-04-01&en=(today)&id=p83403746230)

[![](img/9ab2e01d94fd9436ef8036b81ca3a8d2.png)](http://stockcharts.com/h-sc/ui?s=hyg&p=w&st=2007-04-01&en=(today)&id=p83403746230)

With R we can statistically analyze the similarity of REITs and High Yield.

[R code (click to download):](https://docs.google.com/leaf?id=0B2qp2r96khJPNTQ2ZjNhMjAtZjBmNS00ZWJmLTk5YzEtOGY3MDI4ZWJlMjYy&hl=en_US)

```
#analyze REITs and High Yield   require(quantmod)
require(PerformanceAnalytics)   #get ML/BAC High Yield Index
MLHY <- getSymbols("BAMLHYH0A0HYM2TRIV",src="FRED",auto.assign=FALSE)
#get Wilshire REIT Index
getSymbols("WILLREITIND",src="FRED")   prices <- na.omit(merge(WILLREITIND,MLHY))
colnames(prices) <- c("Wilshire.REIT","MLBAC.HighYield")
returns <- ROC(prices,n=1,type="discrete")   charts.PerformanceSummary(returns,ylog=TRUE,
	main="Wilshire REIT Total Return and ML/BAC High Yield",
	colorset=c("cadetblue","darkolivegreen3"))   chart.TimeSeries(runCor(returns[,1],returns[,2],n=250),
	main="Wilshire REIT Total Return and ML/BAC High Yield
	Rolling 1 Year Correlation",colorset="cadetblue")   chart.Correlation(returns)
```

[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")