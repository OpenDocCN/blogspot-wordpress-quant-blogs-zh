<!--yml

类别：未分类

date: 2024-05-18 15:18:27

-->

# 及时投资组合：1919-2011 年债券回报的历史来源与 Shiller 数据

> 来源：[`timelyportfolio.blogspot.com/2011/04/historical-sources-of-bond-returns-with.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/04/historical-sources-of-bond-returns-with.html#0001-01-01)

一如既往，我总是想要一个更长的数据集，所以在稍微玩了一下 R-Excel 之后，我们可以将债券回报的历史来源延长到 1919 年。否则，也许您可以在 R 中找到[Shiller 数据集](http://www.econ.yale.edu/~shiller/data/ie_data.xls)的其他用途。

作为额外奖励，我们可以准备一个箱形图。

一如既往，请批评或提出建议。

R 代码：

require(quantmod)

require(PerformanceAnalytics)

getSymbols("BAA",src="FRED") #从 Fed Fred 加载信用公司数据

#获取 Shiller 数据通胀和美国国债 10 年

require(gdata)

URL <- "[`www.econ.yale.edu/~shiller/data/ie_data.xls"`](http://www.econ.yale.edu/~shiller/data/ie_data.xls%22)

shillerData <- read.xls(URL,sheet="Data",pattern="Rate GS10")

#删除日期(1)，CPI(5)，GS10(7)

shillerData <- shillerData[,c(1,5,7)]

#从 1919 年 1 月获取数据，以匹配 BAA xts 系列

shillerData <- shillerData[rownames(shillerData[which(shillerData$Date==format(index(BAA)[1],"%Y.%m")):NROW(shillerData),]),2:3]

shillerData <- xts(shillerData[1:NROW(BAA),1:2],order.by=index(BAA))

bondReturnSources<-merge(BAA,shillerData)

bondReturnSources[,1]<-bondReturnSources[,1]-bondReturnSources[,3]

#获取 12 个月的 CPI 变化

bondReturnSources[,2]<-ROC(bondReturnSources[,2],12,type="discrete")*100

bondReturnSources[,3]<-bondReturnSources[,3]-bondReturnSources[,2]

bondReturnSources<-merge(bondReturnSources,bondReturnSources[,1]+bondReturnSources[,2]+bondReturnSources[,3])

colnames(bondReturnSources)<-c("Credit","Inflation","Real","Total")

chart.TimeSeries(bondReturnSources,legend.loc="bottom",main="Historical Sources of Bond Returns",ylab="Yield as %",colorset=c("cadetblue","darkolivegreen3","goldenrod","gray70"))

#添加来源作为标题

mtext("Source: Federal Reserve FRED and Robert Shiller",side=1,adj=0)

chart.Boxplot(bondReturnSources,main="Historical Sources of Bond Returns",colorset=c("cadetblue","darkolivegreen3","goldenrod","gray70"))

mtext("Source: Federal Reserve FRED and Robert Shiller",side=1,adj=0)
