<!--yml
category: 未分类
date: 2024-05-18 15:18:32
-->

# Timely Portfolio: Historical Sources of Bond Returns

> 来源：[http://timelyportfolio.blogspot.com/2011/04/historical-sources-of-bond-returns.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/04/historical-sources-of-bond-returns.html#0001-01-01)

As promised in [Monitoring Sources of Bond Return](http://timelyportfolio.blogspot.com/2011/04/monitoring-sources-of-bond-return.html), we can show more history if we use CPI instead of expected inflation (from the TIP inflation breakeven yield).  Here are the results with history back to 1953.

However, more history includes negative inflation, so I think the chart is a little more clear with a PerformanceAnalytics chart.TimeSeries graph.

R code:

require(quantmod)
require(PerformanceAnalytics)
require(reshape2)
require(ggplot2)

getSymbols("GS10",src="FRED") #load 10yTreasury
getSymbols("BAA",src="FRED") #load Corporate for credit
getSymbols("CPIAUCSL",src="FRED") #load CPI for inflation

bondReturnSources<-na.omit(merge(ROC(CPIAUCSL,12,type="discrete")*100,BAA-GS10,GS10-ROC(CPIAUCSL,12,type="discrete")*100))
bondReturnSources<-merge(bondReturnSources,bondReturnSources[,1]+bondReturnSources[,2]+bondReturnSources[,3]) #add for total
colnames(bondReturnSources)<-c("Inflation","Credit","Real","Total")

chart.TimeSeries(bondReturnSources,legend.loc="bottom",main="Historical Sources of Bond Returns",ylab="Yield as %",colorset=c("darkolivegreen3","cadetblue","goldenrod","gray70"))
#use this for stacked bar, but comes out strange with too many months
#chart.StackedBar(bondReturnSources["1953::"],main="Historical Sources of Bond Returns",ylab="Yield as %",colorset=c("darkgreen","red","blue"))

#use ggplot for consistency with previous plot, but negative makes chart hard to read
bondReturnSourcesToGraph<-data.frame(cbind(as.Date(index(bondReturnSources)),coredata(bondReturnSources[,1:3])))
colnames(bondReturnSourcesToGraph)<-c("Date","Inflation","Credit","Real")
bondReturnSourcesToGraph<-melt(bondReturnSourcesToGraph,id.vars=1)
colnames(bondReturnSourcesToGraph)<-c("Date","ReturnSource","Yield")
rownames(bondReturnSourcesToGraph)<-c(1:NROW(bondReturnSourcesToGraph))
ggplot(bondReturnSourcesToGraph, stat="identity", aes(x=Date,y=Yield,fill=ReturnSource,group=ReturnSource)) + geom_area() +scale_x_date(format = "%Y") + opts(title = "Historical Sources of Bond Return")