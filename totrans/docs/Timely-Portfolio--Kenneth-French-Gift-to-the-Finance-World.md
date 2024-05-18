<!--yml
category: 未分类
date: 2024-05-18 15:13:37
-->

# Timely Portfolio: Kenneth French Gift to the Finance World

> 来源：[http://timelyportfolio.blogspot.com/2011/06/kenneth-french-gift-to-finance-world.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/06/kenneth-french-gift-to-finance-world.html#0001-01-01)

```
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
	paste("Large",colnames(french_momentum)[1:3],sep="."))     #get dates ready for xts index
datestoformat <- rownames(french_momentum)
datestoformat <- paste(substr(datestoformat,1,4),
	substr(datestoformat,5,7),"01",sep="-")   #get xts for analysis
french_momentum_xts <- as.xts(french_momentum[,1:6],
	order.by=as.Date(datestoformat))   french_momentum_xts <- french_momentum_xts/100   #jpeg(filename="performance by momentum and size.jpg",quality=100,width=6.25, height = 5,  units="in",res=96)
charts.PerformanceSummary(french_momentum_xts,ylog=TRUE,
	main="Performance by Kenneth French Size and Momentum
	Monthly Since 1927",
	colorset=c("cadetblue3","cadetblue","cadetblue4",
	"darkolivegreen3","darkolivegreen","darkolivegreen4"))
mtext("Source: http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html",
	side=1,adj=0,cex=0.75)
#dev.off()   #jpeg(filename="rolling performance by momentum and size.jpg",quality=100,width=6.25, height = 5,  units="in",res=96)
chart.RollingPerformance(french_momentum_xts,width=36,
	main="Performance by Kenneth French Size and Momentum
	36 Month Rolling Since 1927",
	legend.loc = "bottomright",
	colorset=c("cadetblue3","cadetblue","cadetblue4",
	"darkolivegreen3","darkolivegreen","darkolivegreen4"))
mtext("Source: http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html",
	side=1,adj=0,cex=0.75)
#dev.off()   #use ggplot2 for boxplot
#could also use chart.Boxplot() from PerformanceAnalytics
df <- as.data.frame(
	cbind(as.Date(index(french_momentum_xts)),
	coredata(french_momentum_xts)))
dfmelt <- melt(df,id.vars=1)
colnames(dfmelt) <- c("date","frenchmomentum","return")
#jpeg(filename="boxplot by momentum and size.jpg",quality=100,width=6.25, height = 5,  units="in",res=96)
ggplot(dfmelt,aes(x=frenchmomentum,y=return,colour=frenchmomentum)) +
	geom_boxplot() + opts(title="Kenneth French Momentum and Size")
#dev.off()
```