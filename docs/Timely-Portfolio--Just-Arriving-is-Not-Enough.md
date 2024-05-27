**<!--yml

类别：未分类

日期：2024-05-18 15:13:13

-->**

# 及时投资组合：仅仅到达是不够的

> 来源：[`timelyportfolio.blogspot.com/2011/07/just-arriving-is-not-enough.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/07/just-arriving-is-not-enough.html#0001-01-01)

当你乘坐飞机旅行时，到达目的地是不够的。几乎所有乘客都希望旅途极度平稳，并愿意牺牲方便和准点到达来确保舒适和 perceived 安全。此外，乘客期望飞行员为他们做出这个决定。像飞行员一样，我作为一名资金经理，觉得我负责客户财务旅程的平稳性。然而，与飞行员不同，我背负着更沉重的负担，因为我的客户在经历任何不适时就可以拉下紧急释放装置。由于恐慌或缺乏信心而退出意味着我的客户可能做出一种经济上致命的决定，要么迟到，要么永远无法到达他们的财务目的地，因此我必须更加谨慎，不要考验我的客户的舒适度。

当旅途顺利时，我的大多数客户并不关心我飞得多快，但当天空多云且颠簸严重时，我需要采取不同的路线（分配）或者根本不飞（持现金）。我宁愿客户稍晚到达，也不愿他们拉下紧急释放装置，最终根本无法到达。飞行员不能控制天气，我也不能控制市场，但我们都必须正确评估情况，并做出牺牲方便和准点到达以换取安全和舒适的到达的决定。

**[聪明资金“与世界最伟大投资者一起反弹”](http://www.smartmoney.com/invest/stocks/bouncing-back-with-the-worlds-greatest-investors-1309909342753/?cid=sm_dailyfinanceRSS)**似乎并不认同我的资金管理理念。在第一位经理比尔·尼 gren（Bill Nygren）身上，我看到“Oakmark 在 2007 年下跌了 4%，在 2008 年更是惨遭 36%的跌幅，”并且这灾难性的回撤贯穿了所有四位经理。最让我困扰的是媒体和投资者是如何迅速原谅他们在危机中的糟糕表现和惨重的回撤。这些投资者既没有预见到也没有控制到需要暂时救助他们的近 10 万亿美元的政治和货币决策。下面是提到的基金的一些情况。这些经理人在 2000-2003 年只是回避了科技股，但什么也没做来避免 2007-2009 年更为严重的灾难。

这对我是无法接受的，我相信这些经理人、他们的投资者以及媒体从上一次危机中学到了什么，而这些错误的宽恕将在下一周期受到惩罚。

[R 代码（点击下载）：](https://docs.google.com/leaf?id=0B2qp2r96khJPYWJhZWZmZjctYjFlNS00MWE0LWFmZjctYzE4ZmFjNGQxMjFk&hl=en_US)

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

[由 Pretty R inside-R.org 创建](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")
