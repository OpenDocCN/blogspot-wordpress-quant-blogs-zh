<!--yml
category: 未分类
date: 2024-05-18 15:16:50
-->

# Timely Portfolio: S&P 500 High Beta and Low Volatility Indexes and Powershares ETFs

> 来源：[http://timelyportfolio.blogspot.com/2011/05/s-500-high-beta-and-low-volatility.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/05/s-500-high-beta-and-low-volatility.html#0001-01-01)

There must be a useful insight, concept, or system provided by the new S&P 500 High Beta and Low Volatility Indexes.  Now with the announcement by Powershares of etfs for these indicies [http://www.invescopowershares.com/volatility/](http://www.invescopowershares.com/volatility/ "http://www.invescopowershares.com/volatility/"), any of these potential insights, concepts, or systems seem viable.  The indexes are available through the S&P website in spreadsheet form

> [http://www.standardandpoors.com/indices/sp-500-low-volatility/en/us/?indexId=spusa-500-usdw-lop-us-l--](http://www.standardandpoors.com/indices/sp-500-low-volatility/en/us/?indexId=spusa-500-usdw-lop-us-l-- "http://www.standardandpoors.com/indices/sp-500-low-volatility/en/us/?indexId=spusa-500-usdw-lop-us-l--<br />") [http://www.standardandpoors.com/indices/sp-500-high-beta/en/us/?indexId=spusa-500-usdw-hbp-us-l--](http://www.standardandpoors.com/indices/sp-500-high-beta/en/us/?indexId=spusa-500-usdw-hbp-us-l--)

or through Bloomberg with SP5HBIT for High Beta and SP5LVIT Low Volatility.

If we apply some basic techniques of relative strength and momentum introduced in previous posts, we can build a switching strategy between the High Beta and Low Volatility Indexes.

Or with the same signals, we can use the relative strength (RS) signal to generate entry and exit signals for the overall S&P 500 index.

R code:

require(quantmod)
require(PerformanceAnalytics)

#don't think it is possible to download directly from S&P
#but can get a spreadsheet to use from
#[http://www.standardandpoors.com/indices/sp-500-low-volatility/en/us/?indexId=spusa-500-usdw-lop-us-l--](http://www.standardandpoors.com/indices/sp-500-low-volatility/en/us/?indexId=spusa-500-usdw-lop-us-l--)
#[http://www.standardandpoors.com/indices/sp-500-high-beta/en/us/?indexId=spusa-500-usdw-hbp-us-l--](http://www.standardandpoors.com/indices/sp-500-high-beta/en/us/?indexId=spusa-500-usdw-hbp-us-l--)
#also these indicies are available through Bloomberg and Reuters
#Bloomberg access with R is possible through RBloomberg

SPHighBetaLowVol<-as.xts(read.csv("sphighbeta-lowvol.csv",row.names=1,stringsAsFactors=FALSE))

SPIndexes<-merge(SPHighBetaLowVol,getSymbols("^GSPC",from="2006-01-03",auto.assign=FALSE)[,4])
SPIndexesReturns<-ROC(SPIndexes,1,type="discrete")
charts.PerformanceSummary(SPIndexesReturns)

#let's try an easy relative strength signal and index filter
#know I can do this better in R but here is my ugly code
#to calculate 125 day or 1/2 year slope of high beta/low vol
width=125
#get relative strength slope of high beta/low vol
for (i in 1:(NROW(SPIndexes)-width)) {
    model<-lm(SPIndexes[i:(i+width),1]/SPIndexes[i:(i+width),2]~index(SPIndexes[i:(i+width)]))
    ifelse(i==1,indexRS<-model$coefficients[2],indexRS<-rbind(indexRS,model$coefficients[2]))
}
indexRS<-xts(cbind(indexRS),order.by=index(SPIndexes)[(width+1):NROW(SPIndexes)])

#get slope of total S&P on shorter term 75 day
width=75
for (i in 1:(NROW(SPIndexes)-width)) {
    model<-lm(SPIndexes[i:(i+width),3]~index(SPIndexes[i:(i+width)]))
    ifelse(i==1,indexSlope<-model$coefficients[2],indexSlope<-rbind(indexSlope,model$coefficients[2]))
}
indexSlope<-xts(cbind(indexSlope),order.by=index(SPIndexes)[(width+1):NROW(SPIndexes)])

signals<-na.omit(merge(lag(indexRS),lag(indexSlope),SPIndexesReturns))
ret<-ifelse(signals[,1]>0&signals[,2]>0,signals[,3],ifelse(signals[,1]<0&signals[,2]>0,signals[,4],0))

perf_compare<-merge(ret,SPIndexesReturns)
#name the columns for charting
colnames(perf_compare)<-c("RotationSystem",colnames(perf_compare)[2:4])
charts.PerformanceSummary(perf_compare,main="Rotation System with S&P Indexes)

#now let's use the RS signal to determine entry exit to overall SP index
#when high volatility is outperforming go long S&P 500
ret<-ifelse(signals[,1]>0,signals[,5],0)
perf_compare<-merge(ret,perf_compare)
colnames(perf_compare)<-c("SP500TacticalBasedOnRS",colnames(perf_compare)[2:5])
charts.PerformanceSummary(perf_compare,main="Systems Comparisons with S&P Indexes)