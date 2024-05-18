<!--yml
category: 未分类
date: 2024-05-18 15:18:27
-->

# Timely Portfolio: Historical Sources of Bond Returns with Shiller Data 1919-2011

> 来源：[http://timelyportfolio.blogspot.com/2011/04/historical-sources-of-bond-returns-with.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/04/historical-sources-of-bond-returns-with.html#0001-01-01)

And as usual, I always want a longer data set, so after a little playing with R-Excel, we can extend our historical sources of bond returns to 1919.  If nothing else, maybe you can find other uses for the [Shiller Dataset](http://www.econ.yale.edu/~shiller/data/ie_data.xls) in R.

And as an added bonus, we can prepare a boxplot.

As always, please criticize or make suggestions.

R code:

require(quantmod)
require(PerformanceAnalytics)

getSymbols("BAA",src="FRED") #load Corporate for credit from Fed Fred

#get Shiller data for inflation and US Treasury 10 year
require(gdata)
URL <- "[http://www.econ.yale.edu/~shiller/data/ie_data.xls"](http://www.econ.yale.edu/~shiller/data/ie_data.xls%22)
shillerData <- read.xls(URL,sheet="Data",pattern="Rate GS10")
#strip out date(1), CPI(5), and GS10(7)
shillerData <- shillerData[,c(1,5,7)]
#get data starting in January 1919 to match with BAA xts series
shillerData <- shillerData[rownames(shillerData[which(shillerData$Date==format(index(BAA)[1],"%Y.%m")):NROW(shillerData),]),2:3]
shillerData <- xts(shillerData[1:NROW(BAA),1:2],order.by=index(BAA))

bondReturnSources<-merge(BAA,shillerData)
bondReturnSources[,1]<-bondReturnSources[,1]-bondReturnSources[,3]
#get 12 month CPI change
bondReturnSources[,2]<-ROC(bondReturnSources[,2],12,type="discrete")*100
bondReturnSources[,3]<-bondReturnSources[,3]-bondReturnSources[,2]
bondReturnSources<-merge(bondReturnSources,bondReturnSources[,1]+bondReturnSources[,2]+bondReturnSources[,3])

colnames(bondReturnSources)<-c("Credit","Inflation","Real","Total")

chart.TimeSeries(bondReturnSources,legend.loc="bottom",main="Historical Sources of Bond Returns",ylab="Yield as %",colorset=c("cadetblue","darkolivegreen3","goldenrod","gray70"))
#add source as caption
mtext("Source: Federal Reserve FRED and Robert Shiller",side=1,adj=0)

chart.Boxplot(bondReturnSources,main="Historical Sources of Bond Returns",colorset=c("cadetblue","darkolivegreen3","goldenrod","gray70"))
mtext("Source: Federal Reserve FRED and Robert Shiller",side=1,adj=0)