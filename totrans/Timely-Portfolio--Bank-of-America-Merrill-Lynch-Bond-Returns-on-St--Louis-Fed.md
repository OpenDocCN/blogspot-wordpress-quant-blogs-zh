<!--yml
category: 未分类
date: 2024-05-18 15:16:54
-->

# Timely Portfolio: Bank of America Merrill Lynch Bond Returns on St. Louis Fed

> 来源：[http://timelyportfolio.blogspot.com/2011/05/bank-of-america-merrill-lynch-bond.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/05/bank-of-america-merrill-lynch-bond.html#0001-01-01)

After all my complaining about proprietary data, the St. Louis Federal Reserve announced today the [availability of Bank of America Merrill Lynch Bond Indicies on their FRED site](http://research.stlouisfed.org/fred2/release?rid=209&filter%5B0%5D=units&filter%5B1%5D=Index).  The data is limited in scope and duration, but accessibility especially through R is wonderful.  Thanks to people I normally don’t thank--Bank of America and the Federal Reserve.

I will show a short example with the Bank of America Corp Master and High Yield Master II Indexes.

I am really excited about figuring out this ggplot2 of PerformanceAnalytics tables, so here are two other examples for those who might not have seen this technique in my earlier posts.

Every time I look at bond indicies, I marvel at their unbelievable 30 year run.  2 down years and 12 up years on the BAC ML Corporate Master truly amazes me.  For more on the 30 year secular bull run in bonds, please see my earlier posts.

R code:

#thank you Bank of America Merrill Lynch and St. Louis Fed for this data

require(quantmod)
require(PerformanceAnalytics)
require(ggplot2)

#get Bank of America Merrill Lynch bond index data from St. Louis Fed
#use auto.assign = FALSE so we can use shorter names
MLCorpMaster<-getSymbols("BAMLCC0A0CMTRIV",src="FRED",auto.assign=FALSE)
MLHYMaster<-getSymbols("BAMLHYH0A0HYM2TRIV", src="FRED", auto.assign=FALSE)
MLBondIndexes<-na.omit(merge(ROC(MLCorpMaster,1,type="discrete"),ROC(MLHYMaster,1,type="discrete")))
colnames(MLBondIndexes)<-c("BAC ML Corporate Master","BAC ML High Yield Master II")

charts.PerformanceSummary(MLBondIndexes,ylog=TRUE,
    colorset=c("cadetblue","darkolivegreen3"),
    main="Bank of America Merrill Lynch Bond Indicies from St. Louis Fed")

#do some downside analysis on monthly returns
MLBondIndexes<-merge(monthlyReturn(MLCorpMaster),monthlyReturn(MLHYMaster))
colnames(MLBondIndexes)<-c("BAC ML Corporate Master","BAC ML High Yield Master II")
downsideTable<-melt(cbind(rownames(table.DownsideRisk(MLBondIndexes)),table.DownsideRisk(MLBondIndexes)))
colnames(downsideTable)<-c("Statistic","BondIndex","Value")
ggplot(downsideTable, stat="identity", aes(x=Statistic,y=Value,fill=BondIndex)) + geom_bar(position="dodge") + coord_flip()

yearReturns<-na.omit(table.CalendarReturns(MLBondIndexes)[,(13:NCOL(table.CalendarReturns(MLBondIndexes)))])
yearReturns<-melt(cbind(rownames(yearReturns),yearReturns))
colnames(yearReturns)<-c("Year","BondIndex","Return")
ggplot(yearReturns, stat="identity", aes(x=Year,y=Return,fill=BondIndex)) + geom_bar(position="dodge")