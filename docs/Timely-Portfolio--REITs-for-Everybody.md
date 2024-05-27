<!--yml

category: 未分类

date: 2024-05-18 15:14:50

-->

# Timely Portfolio: REITs for Everybody

> 来源：[`timelyportfolio.blogspot.com/2011/06/reits-for-everybody.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/06/reits-for-everybody.html#0001-01-01)

**这不是投资建议。这只是我的观点。听取我的意见可能会损失很多钱。**

我认为现在 REITs 有两个买家：股息选择者和贝塔追逐者。贝塔追逐者的需求已经将价格推到了相对和绝对收益率显著高估的水平。

在我对量化策略的乐趣中暂时休息一下[量化策略建设部分 5](http://timelyportfolio.blogspot.com/2011/06/quantstrat-to-build-on-part-5.html)，我想尝试用 R 复制[The Aleph Blog](http://alephblog.com)在 REITs 方面的一些优秀工作[如何使 REITs 获得更多回报](http://alephblog.com/2011/06/04/how-to-make-more-returns-on-reits/ "Permanent Link to How to Make More Returns on REITs")。不幸的是，我周末回家前无法完成，所以我在本文中展示项目的开始，并希望在周末或周一完成。

[R 代码（点击下载）：](https://docs.google.com/leaf?id=0B2qp2r96khJPNWFiMGEyZWMtYjc2YS00OWI3LThiM2UtMzQ0YmIwMWNiYjY5&hl=en_US)

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

[由 Pretty R 在 inside-R.org 创建](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")
