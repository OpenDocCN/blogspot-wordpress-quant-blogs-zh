<!--yml
category: 未分类
date: 2024-05-18 15:17:34
-->

# Timely Portfolio: CPI and US 10y Treasury Extreme –> System Idea

> 来源：[http://timelyportfolio.blogspot.com/2011/05/cpi-and-us-10y-treasury-extreme-system.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/05/cpi-and-us-10y-treasury-extreme-system.html#0001-01-01)

When I see extremes, I feel compelled to explore. The US 10y Treasury yield is at an extreme versus the annualized 3 month CPI rate of change.

Of course, I have to try to build a system around the idea.  While this 3 month CPI rate of change generates a decent signal of entry and exit for the S&P 500, it appears the 6 to 12 month rate of change works better.  Let’s just use US 10y Treasury minus the lagged (since CPI released middle of following month) 9 month rate of change on CPI.  If the 9 month S&P 500 rate of change exceeds this US10y-9monthCPI rate by –5%, then enter a long S&P 500 position.

Results are better than I would have expected, and the degrees of freedom are fairly robust.

For some hindsight optimization, we can add an exit on upside extremes. Magically, 1987 disappears. I don't recommend this hindsight optimization approach unless the concept works on multiple other markets, but the upside extreme would have you out of the S&P 500 currently also. 

I use these for illustrative purposes. In no way am I providing financial advice.  You are responsible for your own profits and losses.

R code:

require(PerformanceAnalytics)
require(quantmod)

getSymbols("CPIAUCNS",src="FRED") #load CPI from Fed Fred
getSymbols("GS10",src="FRED") #load US Treasury 10y from Fed Fred
getSymbols("GS20",src="FRED") #load US Treasury 20y from Fed Fred
getSymbols("GS30",src="FRED") #load US Treasury 30y from Fed Fred
getSymbols("SP500",src="FRED") #load SP500 from Fed Fred

#fill 20y gap from discontinued 20y Treasuries with 30y
GS20["1987-01::1993-09"]<-GS30["1987-01::1993-09"]

SP500<-to.monthly(SP500)[,4]
#get monthly format to yyyy-mm-dd with the first day of the month
index(SP500)<-as.Date(index(SP500))

#subtract the annualized 3mo ROC of CPI from US 10y
US10yMinus3moCPI<-GS10/100-((1+ROC(CPIAUCNS,3))^4-1)
chartSeries(US10yMinus3moCPI,theme="white.mono")

#get the 12 month rate of change on CPI
#subtract the lagged amount from the 10y Treasury
#I retrieved the 20y series also if you would like to use that here
#it does not make much difference
US10yMinusCPI<-GS10/100-lag(ROC(CPIAUCNS,9,type="discrete"),k=1)

signal<-ifelse(ROC(SP500,n=9)-lag(US10yMinusCPI) > -0.05,1,0)

signal<-lag(signal,k=1)
signal[is.na(signal)]<-0

SPreturn<-ROC(SP500,1,type="discrete")  # 1 month SP500 rate of change
SPreturn[1]<-0

SystemReturn<-signal*SPreturn
SystemEquity<-cumprod(1+signal*SPreturn)*coredata(SP500)[1]

return_compare<-merge(SystemReturn,SPreturn)
colnames(return_compare)<-c("SP500 System based on US10y & CPI","SP500")

charts.PerformanceSummary(return_compare,ylog=TRUE,
    main="Performance Comparison of SP500 and System",
    colorset=c("cadetblue","darkolivegreen3"))
chartSeries(SystemEquity,theme="white.mono",log=TRUE,
    TA="addTA(SP500,on=1);addTA(ROC(SP500,n=9)-lag(US10yMinusCPI))",
    name="Performance Comparison of SP500 and System with Signal")

#now with some hindsight optimization to really limit the drawdown
#add an extreme upside filter and 1987 magically disappears
#don't recommend this approach but a good example
signal<-ifelse(ROC(SP500,n=9)-lag(US10yMinusCPI) > -0.05 & ROC(SP500,n=9)-lag(US10yMinusCPI) < 0.2,1,0)

signal<-lag(signal,k=1)
signal[is.na(signal)]<-0

SPreturn<-ROC(SP500,1,type="discrete")  # 1 month SP500 rate of change
SPreturn[1]<-0

SystemReturn<-signal*SPreturn
SystemEquity<-cumprod(1+signal*SPreturn)*coredata(SP500)[1]
return_compare<-merge(SystemReturn,return_compare)
colnames(return_compare)[1]<-"System with Upside filter"

charts.PerformanceSummary(return_compare,ylog=TRUE,
    main="Performance Comparison of SP500 and System with Upside Extreme Limit",
    colorset=c("gray70","darkolivegreen3","cadetblue"))