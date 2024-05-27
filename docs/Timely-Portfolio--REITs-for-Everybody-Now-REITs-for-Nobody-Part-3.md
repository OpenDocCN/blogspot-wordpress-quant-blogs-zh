<!--yml

category: 未分类

date: 2024-05-18 15:14:02

-->

# Timely Portfolio: REITs for Everybody Now REITs for Nobody Part 3

> 来源：[`timelyportfolio.blogspot.com/2011/06/reits-for-everybody-now-reits-for_22.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/06/reits-for-everybody-now-reits-for_22.html#0001-01-01)

```
require(quantmod)
require(PerformanceAnalytics)   #thanks theHausdorffMetric and -Digital Dude- for the comments
#showing how to download, unzip, and access a zip file
my.url="http://web.mit.edu/cre/research/credl/rca/MoodysREAL-2011Q1.zip"
my.tempfile<-paste(tempdir(),"\\moodys-cppi.zip",sep="")
download.file(my.url, my.tempfile, method="auto", quiet = FALSE, mode = "wb",cacheOK = TRUE)
unzip(my.tempfile,exdir = tempdir(),junkpath=TRUE)
moodyscppi <- read.csv(paste(tempdir(),"\\Monthly Returns National - All Properties.csv",sep=""))
#get date ready for xts
moodyscppi[,1] <- paste(moodyscppi[,1],
	ifelse(moodyscppi[,2]<10,paste("0",moodyscppi[,2],sep=""),moodyscppi[,2]),
	"01",sep="-")
moodyscppi <- as.xts(moodyscppi[,3:4],order.by=as.Date(moodyscppi[,1]))   #jpeg(filename="moodys-cppi-performance.jpg",quality=100,width=6.25, height = 5, 
#	units="in",res=96) 
charts.PerformanceSummary(moodyscppi[,2],
	main="Moody's/REAL Commercial Property Price Index")
#dev.off()   getSymbols("WILLREITIND",src="FRED")  #get Wilshire REIT Total Return
getSymbols("WILLREITPR",src="FRED")   #get Wilshire REIT Price
WILLREITIND <- to.monthly(WILLREITIND)[,4]
WILLREITPR <- to.monthly(WILLREITPR)[,4]
index(WILLREITIND) <- as.Date(index(WILLREITIND))
index(WILLREITPR) <- as.Date(index(WILLREITPR))
#merge returns from cppi and reit indexes
cppi_reit <- na.omit(merge(moodyscppi[,2],
	ROC(WILLREITIND,n=1,type="discrete"),
	ROC(WILLREITPR,n=1,type="discrete")))
colnames(cppi_reit) <- c("Moodys/REAL CPPI",
	"Wilshire REIT Total Return","Wilshire REIT Price")
#jpeg(filename="moodys-cppi-reit.jpg",quality=100,width=6.25, height = 5, 
#	units="in",res=96) 
charts.PerformanceSummary(cppi_reit,cex.legend=1.2,
	main="Moodys/REAL CPPI and Wilshire REIT Indexes",
	colorset=c("cadetblue","darkolivegreen3","purple"))
#dev.off()
#jpeg(filename="cppi-reit-rolling.jpg",quality=100,width=6.25, height = 6.25, 
#	units="in",res=96) 
charts.RollingPerformance(cppi_reit,width=12,legend.loc="topleft",cex.legend=1.2,
	main="Moodys/REAL CPPI and Wilshire REIT Indexes
	Rolling 12 Month Return",
	colorset=c("cadetblue","darkolivegreen3","purple"))
#dev.off()
```
