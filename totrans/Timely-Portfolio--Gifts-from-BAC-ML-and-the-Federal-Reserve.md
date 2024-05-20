<!--yml
category: 未分类
date: 2024-05-18 15:16:01
-->

# Timely Portfolio: Gifts from BAC ML and the Federal Reserve

> 来源：[http://timelyportfolio.blogspot.com/2011/05/gifts-from-bac-ml-and-federal-reserve.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/05/gifts-from-bac-ml-and-federal-reserve.html#0001-01-01)

Bank of America Merrill Lynch and the Federal Reserve Bank of St. Louis Fed continue to surprise me with even more gifts.  This time they added Emerging Market Bond Indexes with history back to 1998 (cannot see Asia Pacific Crisis of 1997-1998 but can see Argentina 2001-2002).  Data like this is extremely difficult to attain without significant subscription costs.

Since BAC ML and the Fed took it a step further, I feel equally obligated to extend my post [Bank of America Merrill Lynch Bond Returns on St. Louis Fed](http://timelyportfolio.blogspot.com/2011/05/bank-of-america-merrill-lynch-bond.html) to include some of this newly added data.

R code:

#thank you Bank of America Merrill Lynch and St. Louis Fed for this data

require(quantmod)
require(PerformanceAnalytics)
require(ggplot2)

#get Bank of America Merrill Lynch bond index data from St. Louis Fed
#use auto.assign = FALSE so we can use shorter names
MLAsiaEmCorp<-getSymbols("BAMLEMRACRPIASIATRIV",src="FRED",auto.assign=FALSE)
MLLatAmEmCorp<-getSymbols("BAMLEMRLCRPILATRIV", src="FRED", auto.assign=FALSE)
MLUSCorp<-getSymbols("BAMLCC0A0CMTRIV", src="FRED", auto.assign=FALSE)
MLBondIndexes<-na.omit(merge(ROC(MLAsiaEmCorp,1,type="discrete"),ROC(MLLatAmEmCorp,1,type="discrete"),ROC(MLUSCorp,1,type="discrete")))
colnames(MLBondIndexes)<-c("BAC ML Asia Emerging Corporate","BAC ML Latin America Emerging Corp","BAC ML US Corporate Master")

charts.PerformanceSummary(MLBondIndexes,ylog=TRUE,
    colorset=c("cadetblue","darkolivegreen3","gray70"),
    main="Bank of America Merrill Lynch Bond Indicies from St. Louis Fed")

#do some downside analysis on monthly returns
MLBondIndexes<-merge(monthlyReturn(MLAsiaEmCorp),monthlyReturn(MLLatAmEmCorp),monthlyReturn(MLUSCorp))
colnames(MLBondIndexes)<-c("BAC ML Asia Emerging Corporate","BAC ML Latin America Emerging Corp","BAC ML US Corporate Master")
downsideTable<-melt(cbind(rownames(table.DownsideRisk(MLBondIndexes)),table.DownsideRisk(MLBondIndexes)))
colnames(downsideTable)<-c("Statistic","BondIndex","Value")
ggplot(downsideTable, stat="identity", aes(x=Statistic,y=Value,fill=BondIndex)) + geom_bar(position="dodge") + coord_flip()

#ggplot annual returns
yearReturns<-na.omit(table.CalendarReturns(MLBondIndexes)[,(13:NCOL(table.CalendarReturns(MLBondIndexes)))])
yearReturns<-melt(cbind(rownames(yearReturns),yearReturns))
colnames(yearReturns)<-c("Year","BondIndex","Return")
ggplot(yearReturns, stat="identity", aes(x=Year,y=Return,fill=BondIndex)) + geom_bar(position="dodge")

#ggplot CAPM statistics
capmTable<-melt(cbind(rownames(table.CAPM(MLBondIndexes[,1:2],MLBondIndexes[,3])),table.CAPM(MLBondIndexes[,1:2],MLBondIndexes[,3])))
colnames(capmTable)<-c("Statistic","BondIndex","Return")
ggplot(capmTable, stat="identity", aes(x=Statistic,y=Return,fill=BondIndex)) + geom_bar(position="dodge") + coord_flip()