<!--yml
category: 未分类
date: 2024-05-18 15:19:13
-->

# Timely Portfolio: Long EEM Short IWM-How it Works in 3 Ways

> 来源：[http://timelyportfolio.blogspot.com/2011/03/long-eem-short-iwm-how-it-works-in-3.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/03/long-eem-short-iwm-how-it-works-in-3.html#0001-01-01)

Long EEM Short IWM potentially works in 3 ways:

1) See my last post “[Asian Currency Opportunity](http://timelyportfolio.blogspot.com/2011/03/asian-currency-opportunity.html)” where currency undervaluation means potential gain of 20-50% versus the US$ and 50%-100% versus the Japanese Yen.  However, even absent the undervaluation, the spread offers protection against a declining dollar, for which most US bond, equity, and real estate investors are not well enough hedged.

2) If the currency undervaluation is not enough, EEM offers better growth at a far lower valuation on an equity basis.  These are not the best indicators of value, but they are public, so I can share them here

Emerging and US Small Cap valuation from [Vanguard](https://personal.vanguard.com/us/funds/vanguard/all?sort=name&sortorder=asc)

|  |
| Equity characteristics as of 02/28/2011 |  |  |  |
|  | Emerging Mkts Stk Idx Inv | MSCI Emerging Markets Index Net USD | Small-Cap Index Fund Inv | MSCI US Small Cap 1750 Index |
| Number of stocks | 900 | 796 | 1722 | 1716 |
| Median market cap | $18.6 billion | $18.9 billion | $1.8 billion | $1.8 billion |
| price/earnings ratio | 14.5x | 14.3x | 26.1x | 26.1x |
| price/book ratio | 2.2x | 2.1x | 2.1x | 2.1x |
| return on equity | 21.70% | 21.00% | 10.20% | 10.20% |
| earnings growth rate | 14.30% | 13.70% | 3.80% | 4.00% |

Emerging and US Small Cap valuation stats from [iShares EEM](http://us.ishares.com/product_info/fund/overview/EEM.htm) and [iShares IWM](http://us.ishares.com/product_info/fund/overview/IWM.htm)

| Fundamentals & Risk as of 2/28/2011 |
|  | EEM | IWM |
| 12-Month Yield | 1.41% | 1.09% |
| Price to Earnings Ratio | 18.69 | 27.98 |
| Price to Book Ratio | 3.44 | 3.58 |

3) The spread offers low correlation versus stocks and bonds in a persistently and dangerously high correlation environment.

I’m still not exactly sure how this is calculated, but I thought this offered another look at something statistical, and I feel is not very well covered by other examples.  Points closest to each other on the chart are most related.

R code:

require(quantmod)
require(PerformanceAnalytics)
require(fAssets)

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

Disclosure:  AS ALWAYS, THESE ARE MY OPINIONS AND THE FUTURE IS UNPREDICTABLE.  CONDITIONS CHANGE AND I ADJUST POTENTIALLY WITHOUT DISCLOSURE ON THIS BLOG.  YOU ARE ON YOUR OWN MAKING INVESTMENT DECISIONS, AND IN NO WAY AM I ADVISING YOU.  I TAKE NO RESPONSIBILITY FOR YOUR GAINS OR LOSSES.