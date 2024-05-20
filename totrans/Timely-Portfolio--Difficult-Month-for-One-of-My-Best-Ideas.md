<!--yml
category: 未分类
date: 2024-05-18 15:11:31
-->

# Timely Portfolio: Difficult Month for One of My Best Ideas

> 来源：[http://timelyportfolio.blogspot.com/2011/09/difficult-month-for-one-of-my-best.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/09/difficult-month-for-one-of-my-best.html#0001-01-01)

THIS IS NOT INVESTMENT ADVICE.  MY IDEAS PROBABLY WILL LOSE YOU MONEY, AND I WILL NOT LET YOU KNOW WHEN I CHANGE MY MIND.

Bloomberg’s article “[Asian Currencies Set for Worst Month Since 1997 Crisis Caused IMF Bailouts](http://www.bloomberg.com/news/2011-09-30/asia-currencies-set-for-worst-month-since-97.html)” demonstrates why with all my bearishness I did not make much money this month.  Just as a reminder for the not so faithful readers, [http://timelyportfolio.blogspot.com/2011/05/russell-napier-asip-in-ft-says-emerging.html](http://timelyportfolio.blogspot.com/2011/05/russell-napier-asip-in-ft-says-emerging.html "http://timelyportfolio.blogspot.com/2011/05/russell-napier-asip-in-ft-says-emerging.html") shows why I like long emerging market stocks and short Russell 2000.  However, this trade does not work so well when the currencies get clobbered.  I understand the clobbering in 1997 when Soros and others had control of the Asian currencies, but 15 years 10 trillion since that crisis, the Asian central banks clearly have control of their currencies if they choose to exert that influence.  Billions in outflows are meaningless compared to the trillions sitting in foreign currencies (see post [Join the Reserves](http://timelyportfolio.blogspot.com/2011/07/join-reserves.html)), primarily the US $.

R code:

require(quantmod)

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

par(mfrow=c(4, 3)) #provides 2 columns and 3 rows for charts
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