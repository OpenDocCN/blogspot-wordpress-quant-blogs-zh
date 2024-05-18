<!--yml
category: 未分类
date: 2024-05-18 15:14:50
-->

# Timely Portfolio: REITs for Everybody

> 来源：[http://timelyportfolio.blogspot.com/2011/06/reits-for-everybody.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/06/reits-for-everybody.html#0001-01-01)

**THIS IS NOT INVESTMENT ADVICE.  IT IS SIMPLY MY OPINION.  LISTENING TO MY OPINION MIGHT LOSE LOTS OF MONEY.**

I contend that REITs now have two buyers: dividend pickers and beta chasers.  The beta chasers’ demand has driven prices to significantly overvalued levels considering relative and absolute yields.

As a quick break from my quantstrat fun [A Quantstrat to Build on Part 5](http://timelyportfolio.blogspot.com/2011/06/quantstrat-to-build-on-part-5.html), I thought I would try to replicate in R some of the fine work done by [The Aleph Blog](http://alephblog.com) on REITs [How to Make More Returns on REITs](http://alephblog.com/2011/06/04/how-to-make-more-returns-on-reits/ "Permanent Link to How to Make More Returns on REITs").  Unfortunately, I will not be able to finish before I head home for the weekend, so I will just show the start of the project in this post and hope to finish this weekend or Monday.

[R code (click to download):](https://docs.google.com/leaf?id=0B2qp2r96khJPNWFiMGEyZWMtYjc2YS00OWI3LThiM2UtMzQ0YmIwMWNiYjY5&hl=en_US)

```
require(quantmod)
require(PerformanceAnalytics)
require(stringr)   #get NAREIT data
require(gdata) 
URL <- "http://returns.reit.com/returns/MonthlyHistoricalReturns.xls"
reitData <- read.xls(URL,sheet="Data",pattern="All REITs",stringsAsFactors=FALSE)   #shift colnames over 1
colnames(reitData) <- colnames(reitData)[c(1,1:(NCOL(reitData)-1))]   #get dates and return columns
reitData <- reitData[,c(1,3,24,38)]
#name columns
colnames(reitData) <- c("Date",paste(colnames(reitData)[2:4],".Total.Return",sep=""))
reitData <- reitData[3:NROW(reitData),]
#get in format we can use with xts
datetoformat <- reitData[,1]
datetoformat <- paste(substr(datetoformat,1,3),"-01-",substr(datetoformat,5,6),sep="")
datetoformat <- as.Date(datetoformat,format="%b-%d-%y")
rownames(reitData) <- datetoformat
#eliminate column 2
reitData<-reitData[,2:NCOL(reitData)]
#erase commas
col2cvt <- 1:NCOL(reitData)
reitData[,col2cvt] <- lapply(reitData[,col2cvt],function(x){as.numeric(gsub(",", "", x))}) 
#create xts
reitData <- as.xts(reitData,order.by=datetoformat)   chart.TimeSeries(reitData,ylog=TRUE,legend.loc="topleft",main="NAREIT REIT Monthly Performance")
```

[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")