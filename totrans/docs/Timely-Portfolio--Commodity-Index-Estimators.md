<!--yml
category: 未分类
date: 2024-05-18 15:17:38
-->

# Timely Portfolio: Commodity Index Estimators

> 来源：[http://timelyportfolio.blogspot.com/2011/05/commodity-index-estimators.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/05/commodity-index-estimators.html#0001-01-01)

In this post I will show my first try at a commodity index substitute.  Regular readers know my frustration with proprietary data as I try to demonstrate various techniques to users who might not have the resources to pay for the data.  I have substituted US 10y Treasury Total Returns series as my bond proxy with good results, but I have so far been unable to find a free and readily available substitute for commodity indexes.

PPI is not real-time, but might offer one good 1-month lagged proxy for commodity indexes.  If we use

[PPI data from the St. Louis Federal Reserve FRED system](http://research.stlouisfed.org/fred2/categories/31)

, I can get close, but I am unsure if it will be close enough until further system testing.

R code:

require(PerformanceAnalytics)

require(quantmod)

#getSymbols("NAPMPRI",src="FRED") #load ISM Manufacturing Price

getSymbols("PPIACO",src="FRED") #load PPI All Commodities

getSymbols("PPICRM",src="FRED") #load PPI Crude for Further Processing

getSymbols("PPIIDC",src="FRED") #load PPI Industrial

#unfortunately cannot get substitute for proprietary CRB data

#get data series from csv file

CRB<-as.xts(read.csv("spxcrbndrbond.csv",row.names=1))[,2]

#my CRB data is end of month; could change but more fun to do in R

CRB<-to.monthly(CRB)[,4]

index(CRB)<-as.Date(index(CRB))

#NAPMPRI_change<-ROC(NAPMPRI,1)

PPIACO_change<-ROC(PPIACO,1)

PPICRM_change<-ROC(PPICRM,1)

PPIIDC_change<-ROC(PPIIDC,1)

#combine all Rate of Change series with CRB lag 1 month (moved forward) to account for PPI delay

CRBandPPI<-merge(lag(CRB,k=1),PPIACO_change,PPICRM_change,PPIIDC_change)

colnames(CRBandPPI)<-c("CRB","PPI All Comm","PPI Crude for Further","PPI Industrial")

chart.CumReturns(CRBandPPI,main="CRB Estimators through PPI",legend.loc="topleft")

chart.CumReturns(CRBandPPI["1990::"],main="CRB Estimators through PPI since 1990",legend.loc="topleft")

chart.Correlation(CRBandPPI,main="CRB Estimators through PPI")

chart.Correlation(CRBandPPI["1990::"],main="CRB Estimators through PPI since 1990")