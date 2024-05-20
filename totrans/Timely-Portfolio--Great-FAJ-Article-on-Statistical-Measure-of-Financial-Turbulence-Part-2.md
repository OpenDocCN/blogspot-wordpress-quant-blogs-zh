<!--yml
category: 未分类
date: 2024-05-18 15:18:03
-->

# Timely Portfolio: Great FAJ Article on Statistical Measure of Financial Turbulence Part 2

> 来源：[http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical_26.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical_26.html#0001-01-01)

[![faj abstract](img/83360755bc97c4bdbc31c63f84665b6b.png "faj abstract")](http://www.cfapubs.org/doi/abs/10.2469/faj.v66.n5.3)

I did not intend for this to be a multi-part series, but after some clear thinking at the beach over the weekend, I decided that it needed some more analysis.  For those of you that read the article or know [Mahalanobis distance](http://en.wikipedia.org/wiki/Mahalanobis_distance), the measure I presented in my post [Great FAJ Article on Statistical Measure of Financial Turbulence](http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical.htmlhttp://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical.html) was a derivative of actual Mahalanobis distance.  To close the gap between the actual calculation and my measure, I thought I should show both calculations.

The Mahalanobis calculation here is based on the entire dataset.  Of course, we do not have the luxury of hindsight in trading, so I think my real-time measure works well as displayed by the system shown in the first post.

R code:

require(quantmod)
require(PerformanceAnalytics)

#get data from St. Louis Federal Reserve (FRED)
getSymbols("GS20",src="FRED") #load 20yTreasury; 20y has gap 86-93; 30y has gap in early 2000s
getSymbols("GS30",src="FRED") #load 30yTreasury to fill 20y gap 86-93
#getSymbols("BAA",src="FRED") #load BAA
getSymbols("SP500",src="FRED") #load SP500

#get CRB data from a csv file
CRB<-as.xts(read.csv("crb.csv",row.names=1))[,1]

#fill 20y gap from discontinued 20y Treasuries with 30y
GS20["1987-01::1993-09"]<-GS30["1987-01::1993-09"]

#do a little manipulation to get the data lined up on monthly basis
SP500<-to.monthly(SP500)[,4]
#get monthly format to yyyy-mm-dd with the first day of the month
index(SP500)<-as.Date(index(SP500))
#my CRB data is end of month; could change but more fun to do in R
CRB<-to.monthly(CRB)[,4]
index(CRB)<-as.Date(index(CRB))

#let's merge all this into one xts object; CRB starts latest in 1956
assets<-na.omit(merge(GS20,SP500,CRB))
#use ROC for SP500 and CRB and momentum for yield data
assetROC<-na.omit(merge(momentum(assets[,1])/100,ROC(assets[,2:3],type="discrete")))
#get Covariances and multiply to by 100000 for 20y to sp500 and crb and 1000 for sp500 to crb to standardize
#don't like this manual intervention; next post will use correlation instead
assetCovar<-runCov(assetROC[,1],assetROC[,2],n=2)*100000+runCov(assetROC[,1],assetROC[,3],n=2)*100000+runCov(assetROC[,2],assetROC[,3],n=2)*1000
assetROCSum<-assetROC[,1]+assetROC[,2]+assetROC[,3]
turbulence<-abs(assetCovar*assetROCSum)

Sx <- cov(assetROC)
mahalanobisturbulence <- mahalanobis(assetROC, colMeans(assetROC), Sx)

mahalanobisturbulence<-as.xts(cbind(mahalanobisturbulence))

turbulencecompare<-merge(mahalanobisturbulence,turbulence)
colnames(turbulencecompare)<-c("Mahalanobis","MyEstimate")

chart.TimeSeries(turbulencecompare,main="Mahalanobis Distance Compared to My Measure",
    colorset=c("cadetblue","darkolivegreen3"),legend.loc="topleft")
chart.Correlation(turbulencecompare)