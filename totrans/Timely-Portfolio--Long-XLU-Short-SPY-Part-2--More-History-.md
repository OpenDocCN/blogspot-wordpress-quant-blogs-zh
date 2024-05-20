<!--yml
category: 未分类
date: 2024-05-18 15:15:45
-->

# Timely Portfolio: Long XLU Short SPY Part 2 (More History)

> 来源：[http://timelyportfolio.blogspot.com/2011/05/long-xlu-short-spy-part-2-more-history.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/05/long-xlu-short-spy-part-2-more-history.html#0001-01-01)

**THIS IS NOT INVESTMENT ADVICE.  YOU ARE RESPONSIBLE FOR YOUR OWN GAINS AND LOSSES.**

The Fed is on a roll adding BAC ML Bond Indicies and now complete history for the four primary Dow Jones Indexes, so I wanted to extend my first post [Long XLU Short SPY](http://timelyportfolio.blogspot.com/2011/05/long-xlu-short-spy.html) to add some more historical context.  Unfortunately, the Dow Jones Indicies are only price return, but I think exploration still benefits the discussion.  Including dividends significantly enhances the spread position.

Now with the US 10y Treasury price return series.  See [Historical Sources of Bond Returns-Comparison of Daily to Monthly](http://timelyportfolio.blogspot.com/2011/04/historical-sources-of-bond-returns_17.html) for details on the US 10y Treasury return calculations.

The original discussion was as a bond manager what I can do if I do not like bonds.  Let’s have a quick look at the Long DJUA Short US10y price spread to see how it will work in this context.  Correlations above are certainly attractive.

R code:

#get even more history

require(RQuantLib)
require(PerformanceAnalytics)
require(quantmod)

#first bonds
getSymbols("DGS10",src="FRED") #load daily US Treasury 10y from Fed Fred

DGS10pricereturn<-DGS10  #set this up to hold price returns

DGS10pricereturn[1,1]<-0
colnames(DGS10pricereturn)<-"PriceReturn-daily to monthly DGS10"
#I know I need to vectorize this but not qualified enough yet
#Please feel free to comment to show me how to do this
for (i in 1:(NROW(DGS10)-1)) {
  DGS10pricereturn[i+1,1]<-FixedRateBondPriceByYield(yield=DGS10[i+1,1]/100,issueDate=Sys.Date(),
    maturityDate= advance("UnitedStates/GovernmentBond", Sys.Date(), 10, 3),
    rates=DGS10[i,1]/100,period=2)[1]/100-1
}

#total return will be the price return + yield/12 for one month
DGS10totalreturn<-DGS10pricereturn+lag(DGS10,k=1)/12/100
colnames(DGS10totalreturn)<-"Total Return-daily to monthly DGS10"

#now Dow Jones Indexes
getSymbols("DJIA",src="FRED") #load daily Dow Jones Industrial
getSymbols("DJUA",src="FRED") #load daily Dow Jones Utility

DJUADJIA<-DJUA/DJIA
retDJ<-na.omit(merge(ROC(DJUADJIA,1,type="discrete"),ROC(DJIA,1,type="discrete"),ROC(DJUA,1,type="discrete")))
colnames(retDJ)<-c("DJIA","DJUA","DJUADJIAspread")
charts.PerformanceSummary(retDJ,ylog=TRUE,
    main="DJIA, DJUA, and DJUA/DJIA Spread Price Return Analysis",
    colorset=c("cadetblue","darkolivegreen3","goldenrod"))

#now add bonds to analysis
retToAnalyze<-na.omit(merge(ROC(DJIA,1,type="discrete"),
    ROC(DJUA,1,type="discrete"),
    ROC(DJUA/DJIA,1,type="discrete"),
    DGS10pricereturn))
colnames(retToAnalyze)<-c("DJIA","DJUA","DJUADJIAspread","US10yPrice")
charts.PerformanceSummary(retToAnalyze,ylog=TRUE,
    main="DJIA, DJUA, DJUA/DJIA Spread, and US 10y Price Return Analysis",
    colorset=c("cadetblue","darkolivegreen3","goldenrod","gray70"))
chart.Correlation(retToAnalyze)

corDJUADJIAtoDJIA<-runCor(retDJ[,1],retDJ[,2],120)
corDJUADJIAtoBonds<-runCor(retToAnalyze[,3],retToAnalyze[,4],120)
chartSeries(DJUADJIA,TA="addTA(corDJUADJIAtoDJIA);addTA(corDJUADJIAtoBonds)",
    theme="white",
    name="Long DJUA and Short DJIA with Correlation Analysis")

#now let's see how it looks as long xlu short bonds on price basis
priceBonds<-na.omit(cbind(DGS10pricereturn,rep(1,NROW(DGS10))))
priceBonds<-cumprod(priceBonds[,1]+priceBonds[,2])
DJUABonds<-na.omit(merge(DJUA,priceBonds))
DJUABonds<-DJUABonds[,1]/DJUABonds[,2]
chartSeries(DJUABonds, log=TRUE,
    theme="white",
    name="Long DJUA and Short Bonds Price")