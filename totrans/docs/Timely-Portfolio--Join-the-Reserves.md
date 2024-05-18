<!--yml
category: 未分类
date: 2024-05-18 15:12:47
-->

# Timely Portfolio: Join the Reserves

> 来源：[http://timelyportfolio.blogspot.com/2011/07/join-reserves.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/07/join-reserves.html#0001-01-01)

Most forget that the tremendous macro imbalances caused by the 10 Trillion in foreign reserves are just 14 years old phenomenon but the results have been and will be profound.  The buying started after the Asia Pacific collapse of 1997, and the Asian central banks chose to continuously engage a different form of quantitative easing that far exceeds Bernanke’s QE1 and QE2\. Remember Greenspan’s “Conundrum” and the inability of Fed rate increases to push the long end of the curve higher.  Those artificially restrained rates persuaded money managers and institutions to seek higher returns in new products like CDOs and motivated additional housing demand from the US consumer.  These were both significant factors in the 2008 collapse.

Interest rates are a very effective negative feedback mechanism that helps control the cyclicality of the economy.  When nonmarket forces inhibit the normal functioning of interest rates, significant macro imbalances can cause severe consequences.  Unfortunately, it seems we still have not learned our lesson.

It is very odd to me that all the recent media and popular attention on the political debate gives an illusion of control to our inept politicians and causes us to forget that the market, primarily Asian central bank buyers, determines the limits of US fiscal and monetary policy.  I can only hope that somehow the US can maintain the very tenuous confidence we take for granted.

[R code (click to download):](https://docs.google.com/leaf?id=0B2qp2r96khJPYTVlOWQxNTAtNmRlOC00Y2RkLThhOGUtMTZhMGExZWFlZmFm&hl=en_US)

```
#get reserve data from IMF
require(ggplot2)   url = "http://www.imf.org/external/np/sta/cofer/eng/cofer.csv"   cofer <- read.csv (url, skip=5)
cofer <- cofer[c(7:17),c(1,3:18)]
rownames(cofer) <- cofer[,1]
cofer <- cofer[,2:NCOL(cofer)]
#erase commas
col2cvt <- 1:NCOL(cofer)
cofer[,col2cvt] <- lapply(cofer[,col2cvt],
	function(x){as.numeric(gsub(",", "", x))}) 
#erase spaces
rownames(cofer) <- gsub(" ", "", rownames(cofer))
#get numeric
col2cvt <- 1:NCOL(cofer)
cofer[,col2cvt] <- lapply(cofer[,col2cvt],
	function(x){as.numeric(x)}) 
#get data frame and invert
cofer <- as.data.frame(t(cofer))
#convert years to dates to use
datestoformat <- rownames(cofer)
datestoformat <- as.Date(paste(substr(datestoformat,2,5),"-12-31",sep=""))
#prepare for ggplot
rownames(cofer) <- 1:NROW(cofer)
cofer <- cbind(datestoformat,cofer)
cofer_melt <- melt(cofer,id.vars=1)
colnames(cofer_melt) <- c("Date","Country","Amount")   #get area chart
jpeg(filename="oecd cofer reserves area chart.jpg",quality=100,
	width=6.25, height = 6.25,  units="in",res=96)
ggplot(cofer_melt,
	aes(x=Date,y=Amount,fill=Country)) + geom_area() +
	scale_fill_hue(l=40, c=65) + 
	opts(title="OECD Cofer Foreign Currency Reserves",
		panel.background = theme_rect(colour="gray"))
dev.off()
```

[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")