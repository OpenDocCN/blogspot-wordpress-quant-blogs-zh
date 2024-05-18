<!--yml
category: 未分类
date: 2024-05-18 15:19:24
-->

# Timely Portfolio: Free and Easy Currency Monitor in R

> 来源：[http://timelyportfolio.blogspot.com/2011/03/free-and-easy-currency-monitor-in-r.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/03/free-and-easy-currency-monitor-in-r.html#0001-01-01)

Certainly not the best way to keep up with currencies, but the increasingly important job of monitoring currencies can be free and easy in R using Federal Reserve FRED data.  Here is a template that can be adjusted to your favorite currencies with [symbols listed here](http://research.stlouisfed.org/fred2/categories/94).

See my previous post on how to monitor the [potential US Dollar Collapse cheaply and easily](http://timelyportfolio.blogspot.com/2011/03/death-spiral-warning-graph.html).  Also, currencies are important again, so do not ignore them when investing.  Don’t say I did not warn you and don’t make excuses that you don’t have expensive gear.

R code:

require(quantmod)
require(PerformanceAnalytics)

#get asian currency data from the FED FRED data series
getSymbols("DEXKOUS",src="FRED") #load Korea
getSymbols("DEXMAUS",src="FRED") #load Malaysia
getSymbols("DEXSIUS",src="FRED") #load Singapore
getSymbols("DEXTAUS",src="FRED") #load Taiwan
getSymbols("DEXCHUS",src="FRED") #load China
getSymbols("DEXJPUS",src="FRED") #load Japan
getSymbols("DEXTHUS",src="FRED") #load Thailand
getSymbols("DEXBZUS",src="FRED") #load Brazil
getSymbols("DEXMXUS",src="FRED") #load Mexico
getSymbols("DEXINUS",src="FRED") #load India
getSymbols("DTWEXO",src="FRED") #load US Dollar Other Trading Partners
getSymbols("DTWEXB",src="FRED") #load US Dollar Broad

par(mfrow=c(3, 4)) #provides 4 columns and 3 rows for charts
plot(1/coredata(DEXKOUS["1995::2011"]),type="l",ylab="Korea")
plot(1/coredata(DEXMAUS["1995::2011"]),type="l",ylab="Malaysia")
plot(1/coredata(DEXSIUS["1995::2011"]),type="l",ylab="Singapore")
plot(1/coredata(DEXTAUS["1995::2011"]),type="l",ylab="Taiwan")
plot(1/coredata(DEXCHUS["1995::2011"]),type="l",ylab="China")
plot(1/coredata(DEXJPUS["1995::2011"]),type="l",ylab="Japan")
plot(1/coredata(DEXTHUS["1995::2011"]),type="l",ylab="Thailand")
plot(1/coredata(DEXBZUS["1995::2011"]),type="l",ylab="Brazil")
plot(1/coredata(DEXMXUS["1995::2011"]),type="l",ylab="Mexico")
plot(1/coredata(DEXINUS["1995::2011"]),type="l",ylab="India")
plot(coredata(DTWEXO["1995::2011"]),type="l",ylab="US Dollar Other")
plot(coredata(DTWEXB["1995::2011"]),type="l",ylab="US Dollar Broad")

#if you prefer a prettier chart then you can use
chartSeries(to.monthly(1/DEXSIUS),theme = chartTheme("white"),name="Singapore Dollar/USD",TA="addBBands(10)")