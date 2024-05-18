<!--yml
category: 未分类
date: 2024-05-18 15:18:23
-->

# Timely Portfolio: Historical Bond Price and Total Returns from 10y Yield Series

> 来源：[http://timelyportfolio.blogspot.com/2011/04/historical-bond-price-and-total-returns.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/04/historical-bond-price-and-total-returns.html#0001-01-01)

Without access to Barclays or Merrill Bond Indicies to the 1970s or Ned Davis to 1950, studying historical bond returns is very difficult.  Here is a way to derive price and total returns on the 10 year US Treasury back to 1962.  I would like to extend to 1871, but monthly yields from Shiller and Fed are averages of the daily yields and not month-end values.  Applying this method to these month averages does not work.

R code:

require(RQuantLib)
require(quantmod)
require(PerformanceAnalytics)

getSymbols("DGS10",src="FRED") #load US Treasury 10y from Fed Fred

#Fed monthly series of yields is the monthly average of daily yields
#Shiller series also is monthly average
#to calculate returns monthly average does not work
#so we get daily, take monthend with to.monthly
#and unfortunately the series does not go back as far
DGS10<-to.monthly(DGS10)[,4]
DGS10pricereturn<-DGS10  #set this up to hold price returns

DGS10pricereturn[1,1]<-0
colnames(DGS10pricereturn)<-"PriceReturn"
#I know I need to vectorize this but not qualified enough yet
#Please feel free to comment to show me how to do this
for (i in 1:(NROW(DGS10)-1)) {
  DGS10pricereturn[i+1,1]<-FixedRateBondPriceByYield(yield=DGS10[i+1,1]/100,issueDate=Sys.Date(),
    maturityDate= advance("UnitedStates/GovernmentBond", Sys.Date(), 10, 3),
    rates=DGS10[i,1]/100,period=2)[1]/100-1
}

#total return will be the price return + yield/12 for one month
DGS10totalreturn<-DGS10pricereturn+lag(DGS10,k=1)/12/100
colnames(DGS10totalreturn)<-"Total Return"

charts.PerformanceSummary(merge(DGS10pricereturn,DGS10totalreturn),ylog=TRUE,colorset=c("cadetblue","darkolivegreen3"),main="Simulated Returns from US10y Yield")
mtext("Source: Federal Reserve FRED",side=1,adj=0)