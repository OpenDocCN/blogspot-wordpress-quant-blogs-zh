<!--yml
category: 未分类
date: 2024-05-18 15:16:06
-->

# Timely Portfolio: Russell Napier, ASIP in FT Says Emerging Market Currencies

> 来源：[http://timelyportfolio.blogspot.com/2011/05/russell-napier-asip-in-ft-says-emerging.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/05/russell-napier-asip-in-ft-says-emerging.html#0001-01-01)

Clearly I have succumbed to confirmation bias, since my second favorite presentation from the [CFA Institute Annual Conference](http://annual.cfaconference.org/) this year came from Scotland native Russell Napier, ASIP who shares my views nearly completely [http://video.ft.com/v/946244201001/Long-View-Historian-sees-S-P-fall-to-400](http://video.ft.com/v/946244201001/Long-View-Historian-sees-S-P-fall-to-400 "http://video.ft.com/v/946244201001/Long-View-Historian-sees-S-P-fall-to-400").

As one of the most bearish money managers in [Barron’s Spring Big Money Poll](http://online.barrons.com/article/SB50001424052970204286704576275002828722960.html#articleTabs_panel_article%3D1), I get some strange looks with my forecast for S&P 500 at 900, so I cannot imagine how much resistance he gets with his S&P 500 potential price of 400.  However, given inappropriate responses to the next crisis or Napier’s “the great reset”, 900 to 400 is not entirely inconceivable.

> “Kenton Russell, of the brokerage Sterne Agee, used to be bullish, but now makes no bones about being a bear. "The primary assumption people are making is dollar stability," he says. "If you don't pay attention to the dollar while being long bonds and stocks in the U.S., you are not paying attention to the most crucial element of the trade."
> 
> Based on the declining value of the dollar, which hit a 15-month low Wednesday against the euro, the market is "right back at the lows" seen before the financial crisis, Russell says. He expects stocks to drop about 20% in the next year or so, with investors selling the DJIA down to 9500 and the S&P to 900 as they come to realize the U.S. has "reached the limits of fiscal and monetary policy."
> 
> A 20% correction "is no collapse," Russell says, although some might argue it will feel like one. He recommends shorting the [iShares Russell 2000](http://online.barrons.com/public/quotes/main.html?type=djn&symbol=IWM) exchange-traded fund (IWM) and buying the [iShares MSCI Emerging Markets](http://online.barrons.com/public/quotes/main.html?type=djn&symbol=EEM) ETF (EEM), as he thinks Asian currencies are undervalued.”

We both agree most strongly on our view on emerging market currencies.  In an attempt to link what I heard and learned last week at the conference with my blog and R, I thought I should update my March 2011 post [Long EEM Short IWM-How it Works in 3 Ways](http://timelyportfolio.blogspot.com/2011/03/long-eem-short-iwm-how-it-works-in-3.html).  The idea is easily analyzed in R and very easily pursued even by a retail investor.  For all the details please see the [original post](http://timelyportfolio.blogspot.com/2011/03/long-eem-short-iwm-how-it-works-in-3.html).  Here are the updated charts and a couple of new charts.

R code:

require(quantmod)
require(PerformanceAnalytics)
require(fAssets)
require(ggplot2)

tckr<-c("EEM","IEF","IWM","GLD","SPY")

start<-"2005-01-01"
end<- format(Sys.Date(),"%Y-%m-%d") # yyyy-mm-dd

# Pull tckr index data from Yahoo! Finance
getSymbols(tckr, from=start, to=end)

EEM<-adjustOHLC(EEM,use.Adjusted=T)
IEF<-adjustOHLC(IEF,use.Adjusted=T)
IWM<-adjustOHLC(IWM,use.Adjusted=T)
GLD<-adjustOHLC(GLD,use.Adjusted=T)
SPY<-adjustOHLC(SPY,use.Adjusted=T)

EEM<-to.weekly(EEM, indexAt='endof')
IEF<-to.weekly(IEF, indexAt='endof')
IWM<-to.weekly(IWM, indexAt='endof')
GLD<-to.weekly(GLD, indexAt='endof')
SPY<-to.weekly(SPY, indexAt='endof')
EEMIWM<-to.weekly(EEM/IWM, indexAt='endof')

RetToAnalyze<-merge(weeklyReturn(EEM),weeklyReturn(IEF),weeklyReturn(IWM),weeklyReturn(GLD),weeklyReturn(SPY),weeklyReturn(EEMIWM))
colnames(RetToAnalyze)<-c(tckr,"EEMIWM")

assetsDendrogramPlot(as.timeSeries(RetToAnalyze))
assetsCorEigenPlot(as.timeSeries(RetToAnalyze))
mtext("Source: Yahoo! Finance",side=1,adj=0)

chart.Correlation(RetToAnalyze[,1:6,drop=F], main="Correlation since 2005")
mtext("Source: Yahoo! Finance",side=1,adj=0)

#get Rolling Correlations with IEF(bonds) and SPY(stocks)
corEEMIWMtoBonds<-runCor(RetToAnalyze[,6],RetToAnalyze[,2],25)
corEEMIWMtoStocks<-runCor(RetToAnalyze[,6],RetToAnalyze[,5],25)
chartSeries(EEMIWM,TA="addBBands();addTA(corEEMIWMtoBonds);addTA(corEEMIWMtoStocks)",theme="white")
mtext("Source: Yahoo! Finance",side=1,adj=0)

#downside risk comparison
downsideTable<-melt(cbind(rownames(table.DownsideRisk(RetToAnalyze)),table.DownsideRisk(RetToAnalyze)))
colnames(downsideTable)<-c("Statistic","Portfolio","Value")
ggplot(downsideTable, stat="identity", aes(x=Statistic,y=Value,fill=Portfolio)) + geom_bar(position="dodge") + coord_flip()
mtext("Source: Yahoo! Finance",side=1,adj=0)

chart.Boxplot(RetToAnalyze,main="Box Plot of Various Assets 2005 to May 2011")
mtext("Source: Yahoo! Finance",side=1,adj=0)

assetsRiskReturnPlot(RetToAnalyze)

table.CaptureRatios(RetToAnalyze[,6],RetToAnalyze[,5])
pfolioHist(RetToAnalyze[,6])
assetsMomentsPlot(as.timeSeries(RetToAnalyze), main="Plot of Moments of Various Assets since 2005")