<!--yml
category: 未分类
date: 2024-05-18 15:13:13
-->

# Timely Portfolio: Just Arriving is Not Enough

> 来源：[http://timelyportfolio.blogspot.com/2011/07/just-arriving-is-not-enough.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/07/just-arriving-is-not-enough.html#0001-01-01)

When you fly on an airplane, just arriving at your destination is not enough.  Almost all passengers want the ride to be super smooth and will sacrifice convenience and an on-time arrival to ensure comfort and perceived safety.  Also, passengers expect pilots to make this decision for them.  Like a pilot, I feel as a money manager, I bear the responsibility for the smoothness of my clients’ financial journey.  Unlike a pilot though, I have a much more significant burden since my clients can pull the emergency release as soon as they experience any discomfort.  Exiting due to panic or lack of confidence means my clients possibly make a financially fatal decision and either arrive late or never at their financial destination, so I must be even more cautious to not test the limits of my clients’ comfort.

When the ride is smooth, most of my clients do not care how fast I fly, but when the skies are unclear and the bumps severe, I need to take a different route (allocation) or not fly at all (sit in cash).  I would rather my client arrive a little late than to pull the emergency release and not arrive at all.  Pilots do not control the weather, and I do not control the markets, but we both must properly gauge conditions and make the decision to sacrifice convenience and an on-time arrival for a safe and comforable arrival.

*[Smart Money “Bouncing Back with the World’s Greatest Investors”](http://www.smartmoney.com/invest/stocks/bouncing-back-with-the-worlds-greatest-investors-1309909342753/?cid=sm_dailyfinanceRSS)* does not seem to agree with my money management philosophy.  On the first manager Bill Nygren I see “Oakmark's 4 percent loss in 2007, and to a more dismal drop of 36 percent in 2008,” and these devastating drawdowns persist through the all four managers.  What troubles me most is how quickly the press and investors forgive pitiful performance and awful drawdowns in the crisis. These investors neither foresaw nor controlled the almost $10 trillion in political and monetary decisions required to temporarily rescue them. Here is a look at the mentioned funds.  Most of these managers simply avoided tech stocks in 2000-2003, but did nothing to avoid the far more severe disaster of 2007-2009.

This is unacceptable to me, and I believe the flawed forgiveness will be punished in the next cycle as these managers, their investors, and the press learned nothing from the last crisis.

[R code (click to download):](https://docs.google.com/leaf?id=0B2qp2r96khJPYWJhZWZmZjctYjFlNS00MWE0LWFmZjctYzE4ZmFjNGQxMjFk&hl=en_US)

```
#look at funds run by Smart Money's "world's greatest investors"
#http://www.smartmoney.com/invest/stocks/bouncing-back-with-the-worlds-greatest-investors-1309909342753/?cid=sm_dailyfinanceRSS   require(quantmod)
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
RetWithFrench <-merge(RetToAnalyze,french_momentum_xts[,c(3,6)])     jpeg(filename="performance summary of funds.jpg",quality=100,width=6.25, height = 8,  units="in",res=96)
charts.PerformanceSummary(RetWithFrench["2003-03::2011-05",],ylog=TRUE,
 main="Smart Money World's Greatest Investors???",
 colorset=c("cadetblue","darkolivegreen3","goldenrod",
 "purple","gray","beige"))
dev.off()
```

[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")