<!--yml

category: 未分类

date: 2024-05-18 15:18:32

-->

# Timely Portfolio: 历史债券回报来源

> 来源：[`timelyportfolio.blogspot.com/2011/04/historical-sources-of-bond-returns.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/04/historical-sources-of-bond-returns.html#0001-01-01)

正如在[监控债券回报来源](http://timelyportfolio.blogspot.com/2011/04/monitoring-sources-of-bond-return.html)中所承诺的，如果我们使用消费者价格指数（CPI）而不是预期通胀（来自 TIP 通胀预期收益率），我们可以展示更多的历史数据。以下是自 1953 年以来的历史数据。

然而，更多历史数据包括负通胀，因此我认为使用 PerformanceAnalytics 图表.TimeSeries 图表会使图表更清晰。

R 代码：

require(quantmod)

require(PerformanceAnalytics)

require(reshape2)

require(ggplot2)

getSymbols("GS10",src="FRED") #载入 10 年国债

getSymbols("BAA",src="FRED") #载入企业债券用于信用

getSymbols("CPIAUCSL",src="FRED") #载入 CPI 用于通胀

bondReturnSources<-na.omit(merge(ROC(CPIAUCSL,12,type="discrete")*100,BAA-GS10,GS10-ROC(CPIAUCSL,12,type="discrete")*100))

bondReturnSources<-merge(bondReturnSources,bondReturnSources[,1]+bondReturnSources[,2]+bondReturnSources[,3]) #为总和添加

colnames(bondReturnSources)<-c("Inflation","Credit","Real","Total")

chart.TimeSeries(bondReturnSources,legend.loc="bottom",main="历史债券回报来源",ylab="收益率（%）",colorset=c("darkolivegreen3","cadetblue","goldenrod","gray70"))

#用于堆叠条形图，但月份太多时效果奇怪

#chart.StackedBar(bondReturnSources["1953::"],main="历史债券回报来源",ylab="收益率（%）",colorset=c("darkgreen","red","blue"))

#使用 ggplot 保持与之前图表的一致性，但负值使得图表难以阅读

bondReturnSourcesToGraph<-data.frame(cbind(as.Date(index(bondReturnSources)),coredata(bondReturnSources[,1:3])))

colnames(bondReturnSourcesToGraph)<-c("Date","Inflation","Credit","Real")

bondReturnSourcesToGraph<-melt(bondReturnSourcesToGraph,id.vars=1)

colnames(bondReturnSourcesToGraph)<-c("Date","ReturnSource","Yield")

rownames(bondReturnSourcesToGraph)<-c(1:NROW(bondReturnSourcesToGraph))

ggplot(bondReturnSourcesToGraph, stat="identity", aes(x=Date,y=Yield,fill=ReturnSource,group=ReturnSource)) + geom_area() +scale_x_date(format = "%Y") + opts(title = "历史债券回报来源")
