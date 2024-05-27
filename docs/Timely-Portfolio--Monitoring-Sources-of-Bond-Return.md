<!--yml

类别：未分类

日期：2024-05-18 15:18:36

-->

# Timely Portfolio: Monitoring Sources of Bond Return

> 来源：[`timelyportfolio.blogspot.com/2011/04/monitoring-sources-of-bond-return.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/04/monitoring-sources-of-bond-return.html#0001-01-01)

这是一种监控债券回报来源的方法。在下一版本中，我将使用消费者价格指数（CPI）为系列添加历史数据。

所以现在，你可以从债券中预期大约 5%的回报。那其中有多少是实际回报还不清楚。

R 代码：

require(quantmod)

require(PerformanceAnalytics)

require(reshape2)

require(ggplot2)

getSymbols("WGS10YR",src="FRED") #load 10yTreasury

getSymbols("WFII10",src="FRED") #load 10yTIP for real return

getSymbols("BAMLC0A0CM",src="FRED") #load Corporate for credit

getSymbols("CPIAUCSL",src="FRED") #load Corporate for credit

bondReturnSources<-na.omit(merge(WGS10YR-WFII10,WFII10,to.weekly(BAMLC0A0CM)[,4])["2003::"])

colnames(bondReturnSources)<-c("10yTreasury","10yTIPReal","Credit")

bondReturnSourcesToGraph<-data.frame(cbind(as.Date(index(bondReturnSources)),coredata(bondReturnSources)))

colnames(bondReturnSourcesToGraph)<-c("Date","InflationBreakEven","10yTIPReal","Credit")

bondReturnSourcesToGraph<-melt(bondReturnSourcesToGraph,id.vars=1)

colnames(bondReturnSourcesToGraph)<-c("Date","ReturnSource","Yield")

rownames(bondReturnSourcesToGraph)<-c(1:NROW(bondReturnSourcesToGraph))

ggplot(bondReturnSourcesToGraph, stat="identity", aes(x=Date,y=Yield,fill=ReturnSource,group=ReturnSource)) + geom_area() +scale_x_date(format = "%Y") + opts(title = "Sources of Bond Return")
