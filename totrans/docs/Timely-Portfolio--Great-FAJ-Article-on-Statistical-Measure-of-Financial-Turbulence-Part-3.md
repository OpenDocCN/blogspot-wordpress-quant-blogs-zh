<!--yml
category: 未分类
date: 2024-05-18 15:17:59
-->

# Timely Portfolio: Great FAJ Article on Statistical Measure of Financial Turbulence Part 3

> 来源：[http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical_6197.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical_6197.html#0001-01-01)

Building on posts [Great FAJ Article on Statistical Measure of Financial Turbulence](http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical.html) and [Great FAJ Article on Statistical Measure of Financial Turbulence Part 2](http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical_26.html), I will now build a system incorporating a new correlation-based measure of turbulence and a simple relative strength technique.  First, the new correlation-based measure looks like this

Then if we build a system with just this new correlation-based turbulence, we get fairly good results.  However, if we take one step extra and apply a slope-based relative strength to choose S&P500 or CRB rather than equal-weight both, we get even better results.

I always want more data in countries and years, but 1957 is pretty thorough.  Please let me know how you would improve this system.

R code:

require(quantmod)
require(PerformanceAnalytics)

#get data from St. Louis Federal Reserve (FRED)
getSymbols("GS20",src="FRED") #load 20yTreasury; 20y has gap 86-93; 30y has gap in early 2000s
getSymbols("GS30",src="FRED") #load 30yTreasury to fill 20y gap 86-93
getSymbols("BAA",src="FRED") #load BAA
getSymbols("SP500",src="FRED") #load SP500

#get CRB data from a csv file
CRB<-as.xts(read.csv("crb.csv",row.names=1))[,1]

#fill 20y gap from discontinued 20y Treasuries with 30y
GS20["1987-01::1993-09"]<-GS30["1987-01::1993-09"]

#do a little manipulation to get the data lined up on monthly basis
SP500<-to.monthly(SP500)[,4]
#get monthly format to yyyy-mm-dd with the first day of the month
index(SP500)<-as.Date(index(SP500))
#my CRB data is end of month; could change but more fun to do in R
CRB<-to.monthly(CRB)[,4]
index(CRB)<-as.Date(index(CRB))

#let's merge all this into one xts object; CRB starts last in 1956
assets<-na.omit(merge(GS20,SP500,CRB))
#use ROC for SP500 and CRB and momentum for yield data
assetROC<-na.omit(merge(momentum(assets[,1])/100,ROC(assets[,2:3],type="discrete")))

#get Correlations
corrBondsSp<-runCor(assetROC[,1],assetROC[,2],n=7)
corrBondsCrb<-runCor(assetROC[,1],assetROC[,3],n=7)
corrSpCrb<-runCor(assetROC[,2],assetROC[,3],n=7)
#composite measure of correlations between asset classes and roc-weighted correlations
assetCorr<-(corrBondsSp+corrBondsCrb+corrSpCrb+
    (corrBondsSp*corrSpCrb*assetROC[,2])+
    (corrBondsCrb*corrSpCrb*assetROC[,3])-
    assetROC[,1])/6
#sum of ROCs of asset classes
assetROCSum<-assetROC[,1]+assetROC[,2]+assetROC[,3]
#finally the turbulence measure
turbulence<-abs(assetCorr*assetROCSum*100)
colnames(turbulence)<-"Turbulence-correlation"

chartSeries(turbulence,theme="white",name="Correlation and % Change as Measure of Financial Turbulence")
abline(h=0.8)

chart.ACF(turbulence,main="Auto-correlation of Turbulence")

#wish I could remember where I got some of this code
#most likely candidate is www.fosstrading.com
#please let me know if you know the source
#so I can give adequate credit

#use turbulence to determine in or out of equal-weighted sp500 and crb
signal<-ifelse(turbulence>0.8,0,1)
#use slope of sp500/crb to determine sp500 or crb

signal<-lag(signal,k=1)
# Replace missing signals with no position
# (generally just at beginning of series)
signal[is.na(signal)] <- 0

#get returns from equal-weighted crb and sp500 position; Return.portfolio was causing problems, so did the hard way
ret<-(assetROC[,2]+assetROC[,3])/2
ret[1] <- 0

#get system performance
system_perf<-ret*signal
system_eq<- cumprod(1+ret*signal)

perf_comparison<-merge(lag((assetROC[,2]+assetROC[,3])/2,k=1),system_perf)
colnames(perf_comparison)<-c("Equal-weighted","System-with-turbulence-filter")

charts.PerformanceSummary(perf_comparison,ylog=TRUE,main="Turbulence-based System vs Equal-Weighted CRB and SP500")

#let's use basic relative strength to pick sp500 or crb
#know I can do this better in R but here is my ugly code
#to calculate 12 month slope of sp500/crb
width=12
for (i in 1:(NROW(assets)-width)) {
    model<-lm(assets[i:(i+width),2]/assets[i:(i+width),3]~index(assets[i:(i+width)]))
    ifelse(i==1,assetSlope<-model$coefficients[2],assetSlope<-rbind(assetSlope,model$coefficients[2]))
}
assetSlope<-xts(cbind(assetSlope),order.by=index(assets)[(width+1):NROW(assets)])
#use turbulence to determine in or out of equal-weighted sp500 and crb
signal<-ifelse(turbulence[(width):NROW(turbulence)]>0.8,0,1)

#use slope of sp500/crb to determine sp500 or crb
signal2<-ifelse(assetSlope>0,1,2)

signal<-lag(signal,k=1)
signal[1]<-0
signal2<-lag(signal2,k=1)
signal2[1]<-0

#get sp500 or crb return based on slope
ret<-ifelse(signal2==1,assetROC[(width):NROW(assetROC),2],ifelse(signal2==2,assetROC[(width):NROW(assetROC),3],0))

#get system performance
system_perf_rs<-ret*signal
system_eq_rs<- cumprod(1+ret*signal)

perf_comparison<-merge((assetROC[,2]+assetROC[,3])/2,assetROC[,2],assetROC[,3],system_perf,system_perf_rs)
colnames(perf_comparison)<-c("Equal-weighted","S&P500","CRB","System-with-turbulence-filter","System-with-turbulence-filter and RS")

charts.PerformanceSummary(perf_comparison,ylog=TRUE,main="Turbulence-based System with RS vs Equal-Weighted, CRB, and SP500")