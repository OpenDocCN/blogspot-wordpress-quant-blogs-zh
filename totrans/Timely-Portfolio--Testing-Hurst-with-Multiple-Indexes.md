<!--yml
category: 未分类
date: 2024-05-18 15:14:10
-->

# Timely Portfolio: Testing Hurst with Multiple Indexes

> 来源：[http://timelyportfolio.blogspot.com/2011/06/testing-hurst-with-multiple-indexes.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/06/testing-hurst-with-multiple-indexes.html#0001-01-01)

DO NOT TRADE THIS SYSTEM.  YOU VERY EASILY COULD LOSE LARGE AMOUNTS OF MONEY.

I am not necessarily recommending the system that I presented in [Exploring the Market with Hurst](http://timelyportfolio.blogspot.com/2011/06/exploring-market-with-hurst.html), but I thought it would provide a nice platform to illustrate some backtesting with multiple indexes.  Do not pass on the incredible opportunity presented by almost unlimited indexes from Yahoo! Finance and the Fed.

[R code (click to download):](https://docs.google.com/leaf?id=0B2qp2r96khJPZTIwZWQ4ZWEtYTNlZS00ZDA1LTgxOWMtM2JkZmUyZjZiMWMx&hl=en_US)

```
require(quantmod)
require(PerformanceAnalytics)
require(FGN)   #sort of random mix for additional testing
indexes<-c("STI","KS11","GDAXI","DJUSAU","DJUSFI","RUT","DJUBS")
#iterate through index symbols
for (i in 1:length(indexes))  {
	#get symbol
	getSymbols(paste("^",indexes[i],sep=""),
		from="1900-01-01",to=format(Sys.Date(),"%Y-%m-%d"))
	#set monthly index to first day of the month
	assign(indexes[i],to.monthly(get(indexes[i]))[,4])
	#has to be a cleaner way than this to set the index
	assign(indexes[i],as.xts(coredata(get(indexes[i])),
		order.by=as.Date(index(get(indexes[i])))))
	#get monthly changes
	ret<-ROC(get(indexes[i]),n=1,type="discrete")
	index(ret) <- as.Date(index(ret))
	hurstKmonthly <- apply.rolling(ret, FUN="HurstK", width = 12)
	colnames(hurstKmonthly) <- "HurstK.monthly"
	index(hurstKmonthly) <- as.Date(index(hurstKmonthly))
	serialcorr <- runCor(cbind(coredata(ret)),cbind(index(ret)),n=12)
	serialcorr <- as.xts(serialcorr,order.by=index(ret))
	autoreg <- runCor(ret,lag(ret,k=1),n=12)
	colnames(serialcorr) <- "SerialCorrelation.monthly"
	colnames(autoreg) <- "AutoRegression.monthly"
	signalUpTrend <- runMean(hurstKmonthly+serialcorr+autoreg,n=6) +
		(get(indexes[i])/runMean(get(indexes[i]),n=12)-1)*10
	signalUpTrend <- lag(signalUpTrend,k=1)
	retSys <- merge(ifelse(signalUpTrend > 1, 1, 0) * ret,ret)
	colnames(retSys) <- c(paste(indexes[i]," HurstUp System",sep=""),indexes[i])
	jpeg(filename=paste(indexes[i],".jpg",sep=""),quality=100,width=6.25, height = 5, 
		units="in",res=96) 
 	charts.PerformanceSummary(retSys,ylog=TRUE,cex.legend=1.25,
		colorset=c("cadetblue","darkolivegreen3"))
	dev.off()
}
```

[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")