<!--yml
category: 未分类
date: 2024-05-18 15:22:56
-->

# Timely Portfolio: Japan Intentional or Accidental Pursuit of Deflation

> 来源：[http://timelyportfolio.blogspot.com/2011/02/japan-intentional-or-accidental-pursuit.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/02/japan-intentional-or-accidental-pursuit.html#0001-01-01)

Japan’s intentional or accidental pursuit of deflation has caused an imbalance far greater than Bernanke’s pursuit of inflation.  Japanese policymakers have allowed Yen appreciation versus all other currencies.  It appears that they recognize a couple of things:

> 1) Higher interest rates and inflation represent a much bigger risk to their credit risk, deficit funding, and aging population than deflation.
> 
> 2) Developed markets are saturated by Japanese goods, and further Yen appreciation does not cripple those exports.

However, by recognizing these two items, they are allowing their competition and potential growth engine in the emerging markets to completely take advantage of them.  Hyundai and Samsung in Korea have a 30-50% price advantage over their Japanese competition.

Japan’s desperate attempt to avoid their inevitable collapse from higher rates and inflation is speeding their collapse caused by emerging market competition.  The markets eventually will impose the adjustment to the Japanese situation.  At least Bernanke recognizes the imbalance caused by undervalued Asian currencies and knows that inflation is the only mechanism to force Asian emerging nations to allow their currencies to appreciate to normal valuation even if it means hard decisions for the US eventually.

Lower interest rates encourage imbalances, while higher interest rates force the changes necessary to correct these imbalances.

Since the absolute worst of the Asian collapse in 1997, is Japan better off than the emerging Asian nations?

[![image](img/0ac4daff973fb79db41cac2e7b9f27e8.png "image")](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjzt0po1UovpXVipfSBHgGcAFXBwbnnBaw1usaLEXRTMEyIlLKI0hQcf_962K6QUCQcMVYn4urSMsS_xJ0AhV5_dBG3_9pH8nPZI8FLBtQjYbniY42pVdnXJRtH0Q5UL3hNDk1looHeLg/s1600-h/image%5B22%5D.png)

Since 2007, is Japan better off than the emerging Asian nations?

[![image](img/0484eb574620486e5794a882b9fe52e8.png "image")](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg_zemtkWwQ0FXrEzwsRVIw_uUv3zVv-SvxSza9PMY6lzl0wy30lMVc7p-6aMsakOZ_nYzRfcZQrG1upAU8-R5JRyxl3bUhoKo-7B23Id7HD9myxYwxQf5RSBXMpw4-GAGs2N3Ed-km0Q/s1600-h/image%5B25%5D.png)

As a point of reference, here is [OECD’s calculation of Purchasing Power Parity for the Korea versus Japan](http://www.oecd.org/document/47/0,3746,en_2649_34357_36202863_1_1_1_1,00.html) 184, which means the Korean Won is undervalued versus the Japanese Yen by 84%.  The [Economist’s Big Mac Index](http://www.economist.com/markets/Bigmac/index.cfm) shows undervaluation of Asian currencies versus the Yen to be 40-50%.

The Japanese decision has been treated unkindly in the equity markets

[![](img/035b807bf3f3c6006869cc8e9f4fda3a.png)](http://stockcharts.com/h-sc/ui?s=%24p3dow:%24nikk&p=w&yr=12&mn=6&dy=0&id=p81676149069)

via [StockCharts.com](http://stockcharts.com/h-sc/ui?s=%24p3dow:%24nikk&p=w&yr=12&mn=6&dy=0&id=p81676149069)

For the r geeks here is the code:

require(quantmod)
require(PerformanceAnalytics)

#get asian currency data from the FED FRED data series
getSymbols("DEXKOUS",src="FRED") #load Korea
getSymbols("DEXMAUS",src="FRED") #load Malaysia
getSymbols("DEXSIUS",src="FRED") #load Singapore
getSymbols("DEXTAUS",src="FRED") #load Taiwan
getSymbols("DEXCHUS",src="FRED") #load China
getSymbols("DEXJPUS",src="FRED") #load Japan

asian<-merge(DEXKOUS,DEXMAUS,DEXSIUS,DEXTAUS,DEXCHUS,DEXJPUS)

#do dailyReturn so that I can use pretty PerformanceAnalytics charts
#division puts currencies in Japanese yen from US dollar
asianreturn<-merge(dailyReturn(asian[,6]/asian[,1],subset="1996::"),dailyReturn(asian[,6]/asian[,2],subset="1996::"),dailyReturn(asian[,6]/asian[,3],subset="1996::"),dailyReturn(asian[,6]/asian[,4],subset="1996::"),dailyReturn(asian[,6]/asian[,5],subset="1996::"))

#label columns for graph legends
colnames(asianreturn)<-c("Korea","Malaysia","Singapore","Taiwan","China")

chart.CumReturns(asianreturn,ylim=c(-0.4,0.4),legend.loc="topright",main="Asian Currencies in Japanese Yen",ylab="",period.areas=list(c("Sep 97","Dec 97"),c("Jun 04","Nov 06"),c("Dec 07","Mar 09")),period.color="gray",event.lines=c("Dec 97","Nov 06","Mar 09"),event.labels=c("Asian Tiger Collapse","Carry Trade","Financial Crisis"),event.color="black")
mtext("Source: Federal Reserve FRED",side=1,adj=0)

chart.Drawdown(asianreturn['2006-11-30::',],legend.loc="right",main="Asian Currencies in Japanese Yen",ylab="Drawdown Since Financial Crisis")
mtext("Source: Federal Reserve FRED",side=1,adj=0)

*3.5 hours*