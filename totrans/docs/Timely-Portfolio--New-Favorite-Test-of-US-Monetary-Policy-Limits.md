<!--yml
category: 未分类
date: 2024-05-18 15:18:11
-->

# Timely Portfolio: New Favorite Test of US Monetary Policy Limits

> 来源：[http://timelyportfolio.blogspot.com/2011/04/new-favorite-test-of-us-monetary-policy.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/04/new-favorite-test-of-us-monetary-policy.html#0001-01-01)

After a little additional thought, I discovered that my [Death Spiral Warning Graph](http://timelyportfolio.blogspot.com/2011/03/death-spiral-warning-graph.html) post can be improved through the isolation of the expected inflation component of US 10y yields provided by the US 10y yield – US 10y TIP yield.  Unfortunately, it more accurately reveals the cost of aggressive US Fed monetary policy, and I think offers a more dire assessment of the limits of this policy.

The gains we have experienced seem much more transitory and spurious than a simple chart of the S&P 500 reveals.

R code:

require(quantmod)
require(PerformanceAnalytics)

#get data from St. Louis Federal Reserve (FRED)
getSymbols("DGS10",src="FRED") #load 10yTreasury
getSymbols("DFII10",src="FRED") #load 10yTIP for real return
getSymbols("DTWEXB",src="FRED") #load US dollar
getSymbols("SP500",src="FRED") #load SP500

#new FED monetary policy limit monitor
#US10Y TIP Breakeven Inflation divided by the US Dollar
#old favorite is US 10y Nominal divided by the US Dollar

fedpolicytest<-merge((DGS10-DFII10)/DTWEXB,DGS10/DTWEXB)
colnames(fedpolicytest)<-c("US10yTIPInflationDivByUSDollar (new favorite)","US10yDivByDollar (old favorite)")
chart.TimeSeries(fedpolicytest["2003::2011"],legend.loc="topleft",
    main="US Monetary Policy Test-Does Bernanke Have a Limit?",colorset=c("cadetblue","darkolivegreen3"),ylab="",
    event.lines="2008-07-02",event.labels="July 2, 2008")
#add label to denote new recent high
text(NROW(fedpolicytest["2003::2011"])-15,fedpolicytest[NROW(fedpolicytest),1]+.001,"New High")
#label previous high
abline(h=fedpolicytest["2008-07-02",1],col="cadetblue")