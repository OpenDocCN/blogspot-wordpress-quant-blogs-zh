<!--yml
category: 未分类
date: 2024-05-18 15:18:19
-->

# Timely Portfolio: Historical Sources of Bond Returns-Comparison of Daily to Monthly

> 来源：[http://timelyportfolio.blogspot.com/2011/04/historical-sources-of-bond-returns_17.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/04/historical-sources-of-bond-returns_17.html#0001-01-01)

Thanks so much for the comment on my last post [Historical Bond Price and Total Returns from 10y Yield Series](http://timelyportfolio.blogspot.com/2011/04/historical-bond-price-and-total-returns.html)

> “I know this might sound antithetical to a bond guy, but won't the monthly series get you close enough? “

which proved me wrong and allowed me to get nine additional years of history.  The question caused me to go one step further in proving my statement “…but monthly yields from Shiller and Fed are averages of the daily yields and not month-end values.  Applying this method to these month averages does not work.”  This monthly averaging has caused many problems in the past for me, but in this case, it does not matter.  We can see the difference in monthly averaging (GS10) and month-end daily values (DGS10) in this chart.

However, if we look at the price and total return series from both, the differences are insignificant.

Now that I have cleared that up, I can continue Bond Market as a Casino Game with data back to 1953.

R code:

#do everything twice to compare monthly average to daily

require(RQuantLib)
require(quantmod)
require(PerformanceAnalytics)

getSymbols("DGS10",src="FRED") #load daily US Treasury 10y from Fed Fred
getSymbols("GS10",src="FRED") # load monthly average US 10y from Fed Fred

#Fed monthly series of yields is the monthly average of daily yields
#Shiller series also is monthly average
#to calculate returns monthly average does not work
#so we get daily, take monthend with to.monthly
#and unfortunately the series does not go back as far
DGS10<-to.monthly(DGS10)[,4]
#set index to yyyy-mm-dd format rather than to.monthly mmm yyy for better merging later
index(DGS10)<-as.Date(index(DGS10))
DGS10pricereturn<-DGS10  #set this up to hold price returns
GS10pricereturn<-GS10

DGS10pricereturn[1,1]<-0
colnames(DGS10pricereturn)<-"PriceReturn-daily to monthly DGS10"
#I know I need to vectorize this but not qualified enough yet
#Please feel free to comment to show me how to do this
for (i in 1:(NROW(DGS10)-1)) {
  DGS10pricereturn[i+1,1]<-FixedRateBondPriceByYield(yield=DGS10[i+1,1]/100,issueDate=Sys.Date(),
    maturityDate= advance("UnitedStates/GovernmentBond", Sys.Date(), 10, 3),
    rates=DGS10[i,1]/100,period=2)[1]/100-1
}

GS10pricereturn[1,1]<-0
colnames(GS10pricereturn)<-"PriceReturn-monthly avg GS10"
#I know I need to vectorize this but not qualified enough yet
#Please feel free to comment to show me how to do this
for (i in 1:(NROW(GS10)-1)) {
  GS10pricereturn[i+1,1]<-FixedRateBondPriceByYield(yield=GS10[i+1,1]/100,issueDate=Sys.Date(),
    maturityDate= advance("UnitedStates/GovernmentBond", Sys.Date(), 10, 3),
    rates=GS10[i,1]/100,period=2)[1]/100-1
}

#total return will be the price return + yield/12 for one month
DGS10totalreturn<-DGS10pricereturn+lag(DGS10,k=1)/12/100
colnames(DGS10totalreturn)<-"Total Return-daily to monthly DGS10"
#total return will be the price return + yield/12 for one month
GS10totalreturn<-GS10pricereturn+lag(GS10,k=1)/12/100
colnames(GS10totalreturn)<-"TotalReturn-monthly avg GS10"

chartSeries(DGS10,TA="addTA(GS10,on=1);addTA((DGS10-GS10)/100)",name="Comparison of DGS10 and GS10",theme="white")
mtext("Source: Federal Reserve FRED",side=1,adj=0)

charts.PerformanceSummary(merge(DGS10pricereturn,DGS10totalreturn,GS10pricereturn,GS10totalreturn),ylog=TRUE,colorset=c("cadetblue","darkolivegreen3","goldenrod","gray70"),main="Simulated Returns from US10y Yield")
mtext("Source: Federal Reserve FRED",side=1,adj=0)