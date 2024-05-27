```

分类：未分类

日期：2024-05-18 15:14:10

```

# 及时投资组合：使用多个指数测试赫斯特

> 来源：[`timelyportfolio.blogspot.com/2011/06/testing-hurst-with-multiple-indexes.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/06/testing-hurst-with-multiple-indexes.html#0001-01-01)

不要交易这个系统。你很容易损失大量资金。

我不一定推荐我在[探索市场与赫斯特](http://timelyportfolio.blogspot.com/2011/06/exploring-market-with-hurst.html)中提出的系统，但我觉得这将为展示一些使用多个指数的后向测试提供一个很好的平台。不要错过 Yahoo! Finance 和联邦储备提供的大量指数带来的惊人机会。

[R 代码（点击下载）：](https://docs.google.com/leaf?id=0B2qp2r96khJPZTIwZWQ4ZWEtYTNlZS00ZDA1LTgxOWMtM2JkZmUyZjZiMWMx&hl=en_US)

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

由 Pretty R 在 inside-R.org 创建
