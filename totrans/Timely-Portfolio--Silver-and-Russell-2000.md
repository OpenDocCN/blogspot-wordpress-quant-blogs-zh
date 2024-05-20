<!--yml
category: 未分类
date: 2024-05-18 15:21:44
-->

# Timely Portfolio: Silver and Russell 2000

> 来源：[http://timelyportfolio.blogspot.com/2011/02/silver-and-russell-2000.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/02/silver-and-russell-2000.html#0001-01-01)

When I find a chart that looks like this, I always like to explore a little further.

[![](img/5251def285910c9f45b4b2e17e5a66c7.png)](http://stockcharts.com/h-sc/ui?s=slv&p=d&yr=1&mn=0&dy=0&id=p04441145431)

via [StockCharts.com](http://stockcharts.com/h-sc/ui?s=slv&p=d&yr=1&mn=0&dy=0&id=p04441145431)

I pull it into R and try to find anything worthwhile.  I do not find anything, except that I do not want to be trading both in the same direction and expect any diversification.  But we all know the whole world is correlated.

R code:

require(quantmod)
require(TTR)
require(PerformanceAnalytics)

tckr<-c("GLD","SLV","IWM")

start<-"2006-06-30"
end<- format(Sys.Date(),"%Y-%m-%d") # yyyy-mm-dd

# Pull tckr index data from Yahoo! Finance
getSymbols(tckr, from=start, to=end)

#adjust for splits and dividends
GLD<-adjustOHLC(GLD,use.Adjusted=T)
SLV<-adjustOHLC(SLV,use.Adjusted=T)
IWM<-adjustOHLC(IWM,use.Adjusted=T)

#get daily return from prices to use PerformanceAnalytics
GLD<-dailyReturn(GLD)
SLV<-dailyReturn(SLV)
IWM<-dailyReturn(IWM)

RetToAnalyze<-merge(GLD,SLV,IWM)
colnames(RetToAnalyze)<-tckr

charts.RollingRegression(last(RetToAnalyze,"3 years")[,c(1,2),drop=F],last(RetToAnalyze,"5 years")[,3],legend.loc="topleft",width=20,main="Rolling 20-day Regression")
chart.RollingPerformance(RetToAnalyze,width=150,legend.loc="topleft",main="Rolling 150-day Performance")