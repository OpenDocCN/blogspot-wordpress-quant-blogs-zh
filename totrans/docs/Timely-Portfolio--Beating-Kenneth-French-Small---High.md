<!--yml
category: 未分类
date: 2024-05-18 15:13:26
-->

# Timely Portfolio: Beating Kenneth French Small - High

> 来源：[http://timelyportfolio.blogspot.com/2011/06/beating-kenneth-french-small-high.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/06/beating-kenneth-french-small-high.html#0001-01-01)

```
#the real challenge now is how to beat the best
#small momentum with a system
#get very helpful Ken French data
#for this project we will look at Momentum Portfolios
#http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/ftp/6_Portfolios_ME_Prior_12_2.zip   require(PerformanceAnalytics)
require(quantmod)
require(ggplot2)   my.url="http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/ftp/6_Portfolios_ME_Prior_12_2.zip"
my.tempfile<-paste(tempdir(),"\\frenchmomentum.zip",sep="")
my.usefile<-paste(tempdir(),"\\6_Portfolios_ME_Prior_12_2.txt",sep="")
download.file(my.url, my.tempfile, method="auto", 
	quiet = FALSE, mode = "wb",cacheOK = TRUE)
unzip(my.tempfile,exdir=tempdir(),junkpath=TRUE)
#read space delimited text file extracted from zip
french_momentum <- read.table(file=my.usefile,
	header = TRUE, sep = "",
	as.is = TRUE,
	skip = 12, nrows=1013)
colnames(french_momentum) <- c(paste("Small",
	colnames(french_momentum)[1:3],sep="."),
	paste("Large",colnames(french_momentum)[1:3],sep="."))   #get dates ready for xts index
datestoformat <- rownames(french_momentum)
datestoformat <- paste(substr(datestoformat,1,4),
	substr(datestoformat,5,7),"01",sep="-")   #get xts for analysis
french_momentum_xts <- as.xts(french_momentum[,1:6],
	order.by=as.Date(datestoformat))   french_momentum_xts <- french_momentum_xts/100   charts.PerformanceSummary(french_momentum_xts[,1:3],ylog=TRUE,
	main="Performance by Kenneth French Size and Momentum
	Monthly Since 1927",
	colorset=c("cadetblue3","cadetblue","cadetblue4",
	"darkolivegreen3","darkolivegreen","darkolivegreen4"))
mtext("Source: http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html",
	side=1,adj=0,cex=0.75)
#dev.off()     #get price series of small cap high momentum for system building
french_momentum_price <- cumprod(1+french_momentum_xts[,3])   #speedy solution for ranking from Charles Berry
# http://r.789695.n4.nabble.com/efficient-rolling-rank-td2013535.html
#rolling rank of price over last 12 months (12 means max price for last 12)
#pad first 11 with NA
nper <- 10
x.rank <- c(rep(NA,nper-1),rowSums(coredata(french_momentum_price)[ -(1:(nper-1)) ] >= embed(french_momentum_price,nper)))
x.rank <- as.xts(x.rank,order.by=index(french_momentum_price))
signalRank <- ifelse(x.rank[,1] > 3 | 
	french_momentum_price >= runMax(french_momentum_price,2),1,0)
retRank <- lag(signalRank,k=1)*french_momentum_xts[,3]   #try rolling 10 month moving average popularized by Mebane Faber
signalAvg <- ifelse(french_momentum_price > runMean(french_momentum_price,n=10),1,0)
retAvg <- lag(signalAvg,k=1)*french_momentum_xts[,3]   #try RSI
signalRSI <- ifelse(RSI(french_momentum_price,n=4) > 45,1,0)
retRSI <- lag(signalRSI,k=1)*french_momentum_xts[,3]   retCompare <- merge(retRank,retAvg,retRSI,french_momentum_xts[,3])
colnames(retCompare) <- c("Small.High.Rank",
	"Small.High.Avg","Small.High.RSI","Small.High.Benchmark")
#jpeg(filename="performance of small-high with systems.jpg",quality=100,width=6.25, height = 8,  units="in",res=96)
charts.PerformanceSummary(retCompare,ylog=TRUE,cex.legend=1.2,
	colorset = c("cadetblue","darkolivegreen3","purple","gray70"),
	main="Kenneth French Small Size and High Momentum Stocks
	Compared To Various Price Systems")
#dev.off()   #jpeg(filename="capture of small-high with systems.jpg",quality=100,width=6.25, height = 8,  units="in",res=96)
chart.CaptureRatios(retCompare[,1:3],retCompare[,4],
	main="Kenneth French Small Size and High Momentum Stocks
	Compared To Various Price Systems")
#dev.off()   #get average of small size for additional system testing
french_momentum_avg <- cumprod(1+apply(coredata(french_momentum_xts[,c(1:3)]),MARGIN=1,FUN=mean))
french_momentum_avg <- as.xts(french_momentum_avg,order.by=index(french_momentum_price))
nper <- 10
x.rank <- c(rep(NA,nper-1),rowSums(coredata(french_momentum_avg)[ -(1:(nper-1)) ] >= embed(french_momentum_avg,nper)))
x.rank <- as.xts(x.rank,order.by=index(french_momentum_avg))
signalRankAvg <- ifelse(x.rank[,1] > 3 | 
	french_momentum_price >= runMax(french_momentum_price,2),1,0)
retRankAvg <- lag(signalRankAvg,k=1)*french_momentum_xts[,3]   retCompare <- merge(retRank,retRankAvg,french_momentum_xts[,3])
colnames(retCompare) <- c("Small.High.Rank",
	"Small.High.RankOnAvg","Small.High.Benchmark")
#jpeg(filename="performance of small-high with 2 rank systems.jpg",quality=100,width=6.25, height = 8,  units="in",res=96)
charts.PerformanceSummary(retCompare,ylog=TRUE,cex.legend=1.2,
	colorset = c("cadetblue","darkolivegreen3","gray70"),
	main="Kenneth French Small Size and High Momentum Stocks
	Compared To Rank-based Price Systems")
#dev.off()
```