<!--yml
category: 未分类
date: 2024-05-18 15:13:08
-->

# Timely Portfolio: Drawdown Control Can Also Determine Ending Wealth

> 来源：[http://timelyportfolio.blogspot.com/2011/07/drawdown-control-can-also-determine.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/07/drawdown-control-can-also-determine.html#0001-01-01)

```
#look at funds run by Smart Money's "world's greatest investors"
#http://www.smartmoney.com/invest/stocks/bouncing-back-with-the-worlds-greatest-investors-1309909342753/?cid=sm_dailyfinanceRSS
#then apply a simple moving average system
#to prove a point about controlling drawdown   require(quantmod)
require(PerformanceAnalytics)   tckr<-c("OAKMX","CHTTX","FAIRX","FCNTX")   start<-"1990-01-01"
end<- format(Sys.Date(),"%Y-%m-%d") # yyyy-mm-dd   # Pull tckr index data from Yahoo! Finance
getSymbols(tckr, from=start, to=end, adjust=TRUE)   RetToAnalyze<-merge(dailyReturn(OAKMX),dailyReturn(CHTTX),
 dailyReturn(FAIRX), dailyReturn(FCNTX))
colnames(RetToAnalyze)<-tckr   #get very helpful Ken French data on Momentum Portfolios
#to compare to the funds
#http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/ftp/6_Portfolios_ME_Prior_12_2_Daily.zip   my.url="http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/ftp/6_Portfolios_ME_Prior_12_2_Daily.zip"
my.tempfile<-paste(tempdir(),"\\frenchmomentum.zip",sep="")
my.usefile<-paste(tempdir(),"\\6_Portfolios_ME_Prior_12_2_Daily.txt",sep="")
download.file(my.url, my.tempfile, method="auto", 
 quiet = FALSE, mode = "wb",cacheOK = TRUE)
unzip(my.tempfile,exdir=tempdir(),junkpath=TRUE)
#read space delimited text file extracted from zip
french_momentum <- read.table(file=my.usefile,
 header = TRUE, sep = "",
 as.is = TRUE,
 skip = 12, nrows=12061)
colnames(french_momentum) <- c(paste("Small",
 colnames(french_momentum)[1:3],sep="."),
 paste("Large",colnames(french_momentum)[1:3],sep="."))   #get dates ready for xts index
datestoformat <- rownames(french_momentum)
datestoformat <- paste(substr(datestoformat,1,4),
 substr(datestoformat,5,6),substr(datestoformat,7,8),sep="-")   #get xts for analysis
french_momentum_xts <- as.xts(french_momentum[,1:6],
 order.by=as.Date(datestoformat))
#divide by 100 to get in decimal form
french_momentum_xts <- french_momentum_xts/100   #get column 3 for small momentum and 6 for large momentum
#to compare with the funds
RetWithFrench <-merge(RetToAnalyze,french_momentum_xts[,c(3,6)])   #jpeg(filename="performance summary of funds.jpg",quality=100,width=6.25, height = 8,  units="in",res=96)
#charts.PerformanceSummary(RetWithFrench,ylog=TRUE,
# main="Smart Money World's Greatest Investors???",
# colorset=c("cadetblue","darkolivegreen3","goldenrod",
# "purple","gray","beige"))
#dev.off()   #let's just use a Mebane Faber style 200 day moving average
#to determine entry and exit
#for the best performer CHTTX
signal <- ifelse(CHTTX[,4]>runMean(CHTTX[,4],200),1,0)
signal <- merge(lag(signal,k=1),RetWithFrench[,2])
retCHTTX <- merge(signal[,1] * signal[,2], signal[,2])
colnames(retCHTTX) <- c("CHTTXMeanSystem","CHTTX")
#jpeg(filename="performance summary of chttx and mean system.jpg",quality=100,width=6.25, height = 8,  units="in",res=96)
charts.PerformanceSummary(retCHTTX,ylog=TRUE,
 main="Smart Money World's Greatest Investors???
 CHTTX with 200 Day Mean System",
 colorset=c("cadetblue","purple"))
#dev.off()   #if the investor is comfortable with 60% drawdown
#then they should be comfortable with leverage applied
#to the simple mean system; 2.57 would make them even
#in terms of max drawdown
#jpeg(filename="worst drawdown of chttx and mean system.jpg",quality=100,width=6.25, height = 8,  units="in",res=96)
barplot(maxDrawdown(retCHTTX), main="Worst Drawdown Comparison",
 ylim=c(0,0.6))
dev.off()
#print(maxDrawdown(retCHTTX[,2])/maxDrawdown(retCHTTX[,1]))   #let's see now what it looks like with just 2 times leverage
#applied to the simple mean system
retCHTTX <- merge(signal[,1] * signal[,2], signal[,1] * 2 * signal[,2], signal[,2])
colnames(retCHTTX) <- c("CHTTXMeanSystem","CHTTXMean2xLeverage","CHTTX")
#jpeg(filename="performance summary of chttx and mean system and leverage.jpg",quality=100,width=6.25, height = 8,  units="in",res=96)
charts.PerformanceSummary(retCHTTX,ylog=TRUE,
 main="Smart Money World's Greatest Investors???
 CHTTX with 200 Day Mean System and 2x Leverage",
 colorset=c("cadetblue","darkolivegreen3","purple"))
#dev.off()   #check max drawdown
#now by controlling drawdown we can end up with almost double the money
#with still less total drawdown
#jpeg(filename="worst drawdown of chttx and mean system with leverage.jpg",quality=100,width=6.25, height = 8,  units="in",res=96)
barplot(maxDrawdown(retCHTTX), main="Worst Drawdown Comparison",
 ylim=c(0,0.6))
#dev.off()
jpeg(filename="cumulative return of chttx and mean system with leverage.jpg",quality=100,width=6.25, height = 8,  units="in",res=96)
barplot(Return.cumulative(retCHTTX), main="Cumulative Returns Comparison",
 ylim=c(0,5))
dev.off()
print(Return.cumulative(retCHTTX[,2])/Return.cumulative(retCHTTX[,3]))
```