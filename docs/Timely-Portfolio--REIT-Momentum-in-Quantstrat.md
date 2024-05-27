<!--yml

类别：未分类

日期：2024-05-18 15:14:42

-->

# 及时投资组合：在 Quantstrat 中使用 REIT 动量

> 来源：[`timelyportfolio.blogspot.com/2011/06/reit-momentum-in-quantstrat.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/06/reit-momentum-in-quantstrat.html#0001-01-01)

```
require(quantstrat)
require(PerformanceAnalytics)   # clear out evironment
# much cleaner thanks to Guy Yollin
rm(list=ls())
try(rm(list=ls(pos=.blotter),pos=.blotter),silent=TRUE)
try(rm(list=ls(pos=.strategy),pos=.strategy),silent=TRUE)
try(rm(list=ls(pos=.instrument),pos=.instrument),silent=TRUE)   #set up bucketing function to generate signal
bucket_signal <- function(price,nbuckets,nper) {
	momscore <- price/runMean(price,n=nper)-1	
	breaks <- quantile(momscore, probs = seq(0, 1, 1/nbuckets),na.rm=TRUE)
	buckets <- cut(momscore, breaks=breaks, labels=FALSE)
	signal <- as.xts(buckets,order.by=index(price))	
	colnames(signal) <- "bucket_signal"
	signal[is.na(signal),1] <- 0
	signal
}   #get NAREIT data
#I like NAREIT since I get back to 1971
#see how to get it in previous post
#http://timelyportfolio.blogspot.com/2011/06/reits-for-everybody-might-now-mean.html
#much easier though to get Wilshire REIT since 1977 from FRED
#also it is daily instead of monthly
#i'll use this for simplicity
stock.str <- "WILLREITIND"
getSymbols(stock.str,src="FRED")
#get OHLC all filled with monthly closes
assign(stock.str,to.monthly(get(stock.str)))
index(WILLREITIND) <- as.Date(index(WILLREITIND))
#set up currency and stock
currency('USD')
stock(stock.str,currency='USD',multiplier=1)
initDate='1976-12-31'
initEq=coredata(get(stock.str)[1,4])
tradeSize = 1   #name strategy, account, and portfolio same
name_all <- "momBuckets"
#set up strategy
strat <- strategy(name_all)   #set up portfolio and account
initPortf(name=name_all,symbols=stock.str,initDate=initDate)
initAcct(name=name_all,portfolios=name_all,initDate=initDate,initEq=initEq)
initOrders(portfolio=name_all,initDate=initDate)   #set up indicator
#do bucket indicator
strat <- add.indicator(strategy = strat, name = "bucket_signal",
	arguments=list(price=quote(Cl(mktdata)),nbuckets=5,nper=10),
	label="bucket_signal")
#set up signal
strat <- add.signal(strategy = strat, name="sigThreshold",
	arguments = list(threshold=3,column="bucket_signal",
	relationship="gte",cross=TRUE),
	label="bucket.gte.3")
strat <- add.signal(strategy = strat, name="sigThreshold",
	arguments = list(threshold=3,column="bucket_signal",
	relationship="lt",cross=TRUE),
	label="bucket.lt.3")
#set up rule
strat <- add.rule(strategy=strat,name="ruleSignal",
	arguments = list(sigcol="bucket.gte.3", sigval=TRUE,
	 ordertype='market',orderqty=tradeSize,
	 orderside='long', pricemethod='market', replace=FALSE),
	 type='enter', path.dep=TRUE)
strat <- add.rule(strategy=strat,name="ruleSignal",
	arguments = list(sigcol="bucket.lt.3", sigval=TRUE,
	 orderqty="all", ordertype='market',
	 orderside='long', pricemethod='market', replace=FALSE),
	 type='exit', path.dep=TRUE)   #run strategy and portfolio
out <- applyStrategy(strategy=strat,portfolios=name_all)
#break up steps of applyStrategy for debugging
#strat.ind <- applyIndicators(strategy=strat,mktdata=get(stock.str))
#strat.sig <- applySignals(strategy=strat,indicators=strat.ind)
#applyRules(strategy=strat,portfolio=name_all,symbol=stock.str,
#	indicators=strat.in,Dates=NULL,signals=strat.sig,mktdata=mktdata,path.dep=TRUE)     updatePortf(Portfolio=name_all,Dates=paste('::',as.Date(Sys.time()),sep=''))
#analyze performance
chart.Posn(Portfolio=name_all,Symbol=stock.str)   #unfortunately I do not know yet how to size position
#on each entry to be CurrentEquity/price
#so the compare really is not worthwhile
#this would be the preferred way
#retCompare <- merge(PortfReturns(Account=name_all)/100,
#	ROC(get(stock.str)[,4],n=1,type="discrete"))
#charts.PerformanceSummary(retCompare)     #could do buy/hold comparison similar to
#blog post A Quantstrat to Build On Part 4
#but still not really applicable
#so I will hack this way
#but of course this really defeats the purpose of quantstrat
positions <- getPortfolio(name_all)$symbols$WILLREITIND$posPL[,"Pos.Qty"]
#position of 1 will get return and position of 0 will get nothing
ret <- lag(positions,k=1)*ROC(get(stock.str)[,4],n=1,type="discrete")
retCompare <- merge(ret, ROC(get(stock.str)[,4],n=1,type="discrete"))
colnames(retCompare) <- c("Strategy","Wilshire REIT")
charts.PerformanceSummary(retCompare,ylog=TRUE, cex.legend=1.25,
	main="Wilshire REIT with Aleph Blog Momentum",
	colorset=c("cadetblue","darkolivegreen3"))
```
