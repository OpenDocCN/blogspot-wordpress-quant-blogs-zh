<!--yml

类别：未分类

日期：2024-05-18 15:14:38

-->

# Timely Portfolio: REITs for Everybody Now REITs for Nobody Part 2

> 来源：[`timelyportfolio.blogspot.com/2011/06/reits-for-everybody-now-reits-for.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/06/reits-for-everybody-now-reits-for.html#0001-01-01)

作为对我最初的[REITs for Everybody Might Now Mean REITs for Nobody](http://timelyportfolio.blogspot.com/2011/06/reits-for-everybody-might-now-mean.html)的快速跟进，我想看看 REITs 和高收益债券，这些也可能同时吸引保守的收益买家和对冲的 beta 追逐者。

[HYG (iShares High Yield) and IYR (iShares REIT)](http://stockcharts.com/h-sc/ui?s=hyg&p=w&st=2007-04-01&en=(today)&id=p83403746230)

![](http://stockcharts.com/h-sc/ui?s=hyg&p=w&st=2007-04-01&en=(today)&id=p83403746230)

使用 R 我们可以统计地分析 REITs 和高收益债券之间的相似性。

[R 代码（点击下载）：](https://docs.google.com/leaf?id=0B2qp2r96khJPNTQ2ZjNhMjAtZjBmNS00ZWJmLTk5YzEtOGY3MDI4ZWJlMjYy&hl=en_US)

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

[由 Pretty R 在 inside-R.org 创建](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")
