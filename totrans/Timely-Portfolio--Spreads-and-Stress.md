<!--yml
category: 未分类
date: 2024-05-18 15:15:53
-->

# Timely Portfolio: Spreads and Stress

> 来源：[http://timelyportfolio.blogspot.com/2011/05/spreads-and-stress.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/05/spreads-and-stress.html#0001-01-01)

Since we have the [Gifts from BAC ML and the Federal Reserve](http://timelyportfolio.blogspot.com/2011/05/gifts-from-bac-ml-and-federal-reserve.html), I thought I should look at another interesting element of bonds.  Bond spreads act as a very strong symbol of financial stability and confidence.  The St. Louis Fed Stress Index is weekly, but maybe we can use spreads as a daily proxy of stress or financial instability similar to the [Bloomberg Financial Conditions Index (BFCIUS)](http://www.bloomberg.com/apps/quote?ticker=BFCIUS:IND) nicely explained at [http://www.ssc.wisc.edu/~mchinn/fcw_sep112009.pdf](http://www.ssc.wisc.edu/~mchinn/fcw_sep112009.pdf "http://www.ssc.wisc.edu/~mchinn/fcw_sep112009.pdf") and [www.princeton.edu/~mwatson/papers/MPF_paper_April_13.pdf](http://www.princeton.edu/~mwatson/papers/MPF_paper_April_13.pdf).

If we plot the values from the BAC ML Emerging Market and High Yield Spreads and the St. Louis Fed Index, it is hard to distinguish the lines.

Just for the ggplot2 fans

Correlations total and rolling look like this.

Like volatility and [financial turbulence](http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical_6197.html), periods of extremes are autocorrelated.

And just for fun, here is a chart of the higher moments.

If you want a challenge, tie this spread data to my post [Wonderful New Blog TimeSeriesIreland](http://timelyportfolio.blogspot.com/2011/05/wonderful-new-blog-timeseriesireland.html) or [Great FAJ Article on Statistical Measure of Financial Turbulence Part 3](http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical_6197.html).  Don’t think I have it in me before the weekend.

R code:

#thank you Bank of America Merrill Lynch and St. Louis Fed for this data

require(quantmod)
require(PerformanceAnalytics)
require(ggplot2)

#get Bank of America Merrill Lynch bond index data from St. Louis Fed
#use auto.assign = FALSE so we can use shorter names
MLEmCorpSpreads<-getSymbols("BAMLEMCBPIOAS",src="FRED",auto.assign=FALSE)
MLHYCorpSpreads<-getSymbols("BAMLH0A0HYM2",src="FRED",auto.assign=FALSE)
getSymbols("STLFSI",src="FRED")  #get St.Louis Fed Stress Index

spreadsStress<-na.omit(merge(MLEmCorpSpreads,MLHYCorpSpreads,STLFSI))
colnames(spreadsStress)<-c("BAC ML Emerging","BAC ML HY","St Louis Fed Stress")
chart.TimeSeries(spreadsStress,colorset=c("cadetblue","darkolivegreen3","gray70"),
    legend.loc="topleft",
    main="Bank of America Merrill Lynch Bond Spreads and St. Louis Fed Stress Index")

#chart changes of Spreads and Stress
spreadsStress<-na.omit(merge(momentum(MLEmCorpSpreads,5),momentum(MLHYCorpSpreads,5),momentum(STLFSI,1)))
colnames(spreadsStress)<-c("BAC ML Emerging","BAC ML HY","St Louis Fed Stress")
chart.TimeSeries(spreadsStress,colorset=c("cadetblue","darkolivegreen3","gray70"),
    legend.loc="topleft",
    main="Bank of America Merrill Lynch Bond Spreads and St. Louis Fed Stress Index")
#for the ggplot fans
spreadsStressDf<-data.frame(index(spreadsStress),coredata(spreadsStress))
colnames(spreadsStressDf)<-c("Date",colnames(spreadsStress))
spreadsStressDf<-melt(spreadsStressDf,id.var="Date")
colnames(spreadsStressDf)<-c("Date","Index","Value")
ggplot(spreadsStressDf, stat="identity", aes(x=Date,y=Value,colour=Index)) + geom_line() +
    scale_x_date(format = "%Y") +
    opts(title = "Bank of America Merrill Lynch Bond Spreads and St. Louis Fed Stress Index")
#chart correlations
chart.Correlation(spreadsStress,main="Bank of America Merrill Lynch Bond Spreads and St. Louis Fed Stress Index Correlation")

#explore autocorrelation lags
par(mfrow=c(3,1))  #3 rows and 1 column
acf(spreadsStress[,1],main=colnames(spreadsStress)[1])
acf(spreadsStress[,2],main=colnames(spreadsStress)[2])
acf(spreadsStress[,3],main=colnames(spreadsStress)[3])

#get rolling correlations
corHYStress<-runCor(spreadsStress[,3],spreadsStress[,1],n=20)
corEmStress<-runCor(spreadsStress[,3],spreadsStress[,2],n=20)
corAll<-merge(corHYStress,corEmStress)
chart.TimeSeries(corAll,main="Rolling 20 Week Correlation between Spreads and Stress",
    legend.loc="topright", colorset=c("cadetblue","darkolivegreen3"))

#look at the higher moments
higherMoments<-table.HigherMoments(spreadsStress[,1:2],spreadsStress[,3])
higherMoments<-melt(cbind(rownames(higherMoments),higherMoments))
colnames(higherMoments)<-c("Moment","Index","Value")
ggplot(higherMoments, stat="identity", aes(x=Moment,y=Value,fill=Index)) +
    geom_bar(position="dodge") + coord_flip() +
    opts(legend.position=c(.75,0.88)) #thanks for the tip timeseriesireland