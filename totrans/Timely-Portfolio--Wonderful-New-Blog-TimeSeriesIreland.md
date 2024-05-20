<!--yml
category: 未分类
date: 2024-05-18 15:15:57
-->

# Timely Portfolio: Wonderful New Blog TimeSeriesIreland

> 来源：[http://timelyportfolio.blogspot.com/2011/05/wonderful-new-blog-timeseriesireland.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/05/wonderful-new-blog-timeseriesireland.html#0001-01-01)

I returned from Scotland to find a wonderful new blog from Ireland [http://timeseriesireland.wordpress.com](http://timeseriesireland.wordpress.com).  To highlight his work, I thought I would apply his most recent post [AIB Stock Price, EGARCH-M, and rgarch](http://timeseriesireland.wordpress.com/2011/05/17/aib-stock-price-egarch-m-and-rgarch/) to the S&P 500.  Clearly the author of TimeSeriesIreland has a much better grasp of time series statistics than I do, so I will not attempt to change lag orders or perfect the model.  Rather I will use his model specifications for AIB daily data for S&P 500 weekly data.  This should be fun; maybe this will provoke some comments.

And, it is a shame that I need to disclaim, but **THIS IS FOR ILLUSTRATIVE PURPOSES ONLY AND SHOULD NOT BE CONSIDERED INVESTMENT ADVICE.  YOU ARE RESPONSIBLE FOR YOUR OWN GAINS AND LOSSES.**  I built a very basic system around the fittedmodel$z just for fun.  Here are the results.

R code:

#all credit for this code goes to the very insightful author
#of [http://timeseriesireland.wordpress.com](http://timeseriesireland.wordpress.com)
#based on the first couple of posts I look forward to following him
#for explanation of the statistics and their use, please see
#[http://timeseriesireland.wordpress.com/2011/05/17/aib-stock-price-egarch-m-and-rgarch/#more-295](http://timeseriesireland.wordpress.com/2011/05/17/aib-stock-price-egarch-m-and-rgarch/#more-295)

#I change the code to use SP500 weekly xts data instead of AIB daily tseries data

require(rgarch)
require(urca)
require(ggplot2)
require(quantmod)
require(PerformanceAnalytics)

#define start and end dates
start<-"1929-01-01"
end<- format(Sys.Date(),"%Y-%m-%d") # yyyy-mm-dd

tckr<-"^GSPC"
#use quantmod to get SP500 data
getSymbols(tckr,from=start,to=end)
GSPC<-to.weekly(GSPC)

#get log returns, could also use ROC with type = "continuous"
LGSPC<-log(GSPC[,4])
retGSPC<-diff(LGSPC)

#data frame allows us to use ggplot with date data from xts
#I have not found any better way to ggplot xts data
df1<-data.frame(index(GSPC),coredata(GSPC[,4]))
colnames(df1)<-c("dates","sp500")

### Plot sp500 price:
gg1.1<-ggplot(df1,aes(dates,sp500)) + xlab(NULL) + ylab("SP500 log Price") + scale_y_log10()
gg1.2<-gg1.1+geom_line(colour="darkblue") + opts(title="Weekly SP500 Price 1950-current")
gg1.2

#set first return to 0
retGSPC[1]<-0

df2<-data.frame(index(retGSPC),coredata(retGSPC))
colnames(df2)<-c("dates","sp500")

gg2.1<-ggplot(df2,aes(dates,sp500)) + xlab(NULL) + ylab("Log Changes")
gg2.2<-gg2.1+geom_line(colour="darkred") + opts(title="Weekly SP500 Price Return")
gg2.2

### ACFs and PACFs
par(mfrow=c(2,1))
acf(retGSPC, main="ACF of SP500 Log Returns", lag = 50)
pacf(retGSPC, main="PACF of SP500 Log Returns", lag = 50)

ar9<-arima(retGSPC, order=c(9,0,0))
acf(ar9$residuals)

ressq<-(ar9$residuals)^2

Box.test(ressq, lag = 8, type = "Ljung-Box")

pacf(ressq, main="PACF of Squared Residuals", lag = 30)

# Note that the GARCH order is revered from what I have discussed above
specm1 <- ugarchspec(variance.model=list(model="eGARCH", garchOrder=c(2,4), submodel = NULL),
        mean.model=list(armaOrder=c(9,0), include.mean=TRUE, garchInMean = TRUE))
#this might take a while
fitm1 <- ugarchfit(data = retGSPC, spec = specm1)
fitm1
#plot(fitm1) #use option 8

fittedmodel <- fitm1@fit
sigma1<-fittedmodel$sigma

df2<-data.frame(index(retGSPC),coredata(retGSPC),sigma1)
colnames(df2)<-c("dates","sp500","sigma1")

gg3.1<-ggplot(df2,aes(dates)) + xlab(NULL) + ylab("Log Changes")
gg3.2<-gg3.1+geom_line(aes(y = sp500, colour="Log Returns")) + opts(title="Weekly Log Return with 2 Conditional Standard Deviations")
gg3.3<-gg3.2 + geom_line(aes(y = sigma1*2, colour="2 S.D.")) + geom_line(aes(y = sigma1*-2, colour="2 S.D.")) + scale_colour_hue("Series:") + opts(legend.position=c(.18,0.8))
gg3.3

fitm2 <- ugarchfit(data = retGSPC,out.sample = 10, spec = specm1)
fitm2
pred <- ugarchforecast(fitm2, n.ahead = 10,n.roll = 0)
pred.fpm <- fpm(pred)
pred.fpm

#just because I cannot stand it
#I'll play with a system
#not something I would bet my money on
signal<-runMean(as.xts(fittedmodel$z,order.by=index(retGSPC)),50)
#chartSeries(signal)
signal<-lag(signal,k=1)
signal[is.na(signal)]<-0

ret<-ifelse(signal > 0,ROC(GSPC[,4],1,type="discrete"),0)
returnCompare<-merge(ret,ROC(GSPC[,4],1,type="discrete"))
colnames(returnCompare)<-c("ZSystem","SP500")
charts.PerformanceSummary(returnCompare,ylog=TRUE,main="Just for Fun Z System")