<!--yml

分类：未分类

日期：2024-05-18 15:14:54

-->

# 及时投资组合：构建量化策略（第五部分）

> 来源：[`timelyportfolio.blogspot.com/2011/06/quantstrat-to-build-on-part-5.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/06/quantstrat-to-build-on-part-5.html#0001-01-01)

```
#thanks so much to the developers of quantstrat
#99% of this code comes from the demos in the quantstrat package   #in this I add a variation of the CUD portfolio
#with standard deviations and compare the CUD
#and the new CUDsd   require(quantstrat)   #now let's define our silly countupdown function
CUD <- function(price,n) {
	#CUD takes the n-period sum of 1 (up days) and -1 (down days)
	temp <- runSum(ifelse(ROC(price,1,type="discrete") > 0,1,-1),n)
	colnames(temp) <- "CUD"
	temp
}   #since I've had some very prescient comments
#about standard deviations I'll go ahead and try an sd sum system
CUDsd <- function(price,nsd,nsum) {
	#CUDsd takes the n-period sum of standard deviations
	#feel free to substitute runMAD with runSD if you would like
	temp <- ROC(price,1,type="discrete")/runMAD(ROC(price,1,type="discrete"),n=nsd)
	#bollinger band style sum - uncomment next line
	#temp <- (price-runMedian(price,n=10)-1)/runMAD(ROC(price,1,type="discrete"),n=nsd)
	#doesn't help but if you want to experiment with summing only a n*sd move
	#uncomment and mess with the numbers
	#temp <- ifelse(abs(temp)>1,temp,0)
	temp <- runSum(temp,n=nsum)
	colnames(temp) <- "CUDsd"
	temp
}   #I added this BuyHold as an example; see previous post
#quantstrat version 4 for details
#here is the remnant function
#BuyHold <- function(price,periodtobuy) {
#	#just enter true (1) the period specified as buy and hold
#	#for the remainder
#	temp <- as.xts(rep(0,NROW(price)),order.by=index(price))
#	colnames(temp) <- "BuyHold"
#	temp[periodtobuy,1]<-1
#	temp
#}   try(rm("order_book.CUD",pos=.strategy),silent=TRUE)
try(rm("order_book.CUDsd",pos=.strategy),silent=TRUE)
try(rm("account.CUD","portfolio.CUD",pos=.blotter),silent=TRUE)
try(rm("account.CUDsd","portfolio.CUDsd",pos=.blotter),silent=TRUE)
try(rm("port.st","port.stsd","symbols","symbol","stratCUD","stratCUDsd",
	"initDate","initEq",'start_t','end_t','num_periods'),silent=TRUE)   #specify this for the rolling periods to use for our signal
num_periods=50
#specify these for the CUDsd function
#I separated the sd period from the sum period
#if anyone wants to fool around with the degrees of freedom
num_periods_sd=50
num_periods_sum=50   # Initialize a strategy object
stratCUD <- strategy("CUD")
# Add an indicator
stratCUD <- add.indicator(strategy = stratCUD, name = "CUD", 
	arguments = list(price = quote(Cl(mktdata)),n=num_periods),
	label="CUD")
# enter when CUD > 0
stratCUD <- add.signal(strategy = stratCUD, name="sigThreshold",
	arguments = list(threshold=0, column="CUD",relationship="gte", cross=TRUE),
	label="CUD.gte.0")
# exit when CUD < 0
stratCUD <- add.signal(strategy = stratCUD, name="sigThreshold",
	arguments = list(threshold=0, column="CUD",relationship="lt",cross=TRUE),
	label="CUD.lt.0")
stratCUD <- add.rule(strategy = stratCUD, name='ruleSignal', 
	arguments = list(sigcol="CUD.gte.0", sigval=TRUE, orderqty=1000, ordertype='market',
	 orderside='long', pricemethod='market', replace=FALSE), type='enter', path.dep=TRUE)
stratCUD <- add.rule(strategy = stratCUD, name='ruleSignal', 
	arguments = list(sigcol="CUD.lt.0", sigval=TRUE, orderqty='all',
	 ordertype='market', orderside='long', pricemethod='market', replace=FALSE),
	 type='exit', path.dep=TRUE)   # Initialize a strategy object for the new CUDsd
stratCUDsd <- strategy("CUDsd")
# Add an indicator
stratCUDsd <- add.indicator(strategy = stratCUDsd, name = "CUDsd", 
	arguments = list(price = quote(Cl(mktdata)),nsd=num_periods_sd,nsum=num_periods_sum),
	label="CUDsd")
# enter when CUDsd > 0
stratCUDsd <- add.signal(strategy = stratCUDsd, name="sigThreshold",
	arguments = list(threshold=0, column="CUDsd",relationship="gte", cross=TRUE),
	label="CUDsd.gte.0")
# exit when CUDsd < 0
stratCUDsd <- add.signal(strategy = stratCUDsd, name="sigThreshold",
	arguments = list(threshold=0, column="CUDsd",relationship="lt",cross=TRUE),
	label="CUDsd.lt.0")
stratCUDsd <- add.rule(strategy = stratCUDsd, name='ruleSignal', 
	arguments = list(sigcol="CUDsd.gte.0", sigval=TRUE, orderqty=1000, ordertype='market',
	 orderside='long', pricemethod='market', replace=FALSE), type='enter', path.dep=TRUE)
stratCUDsd <- add.rule(strategy = stratCUDsd, name='ruleSignal', 
	arguments = list(sigcol="CUDsd.lt.0", sigval=TRUE, orderqty='all',
	 ordertype='market', orderside='long', pricemethod='market', replace=FALSE),
	 type='exit', path.dep=TRUE)   currency("USD")
symbols = c("GSPC","GDAXI")
for (symbol in symbols) {
	stock(symbol, currency="USD",multiplier=1)
	#use paste with ^ to get index data
	getSymbols(paste("^",symbol,sep=""),adjust=T,from="1900-12-31")
	assign(symbol,to.weekly(get(symbol)))
}   initDate='1949-12-31'
initEq=1000000
port.st<-'CUD' #use a string here for easier changing of parameters and re-trying
port.stsd <- 'CUDsd'   initPortf(port.st, symbols=symbols, initDate=initDate, initEq=initEq)
initAcct(port.st, portfolios=port.st, initDate=initDate, initEq=initEq)
initOrders(portfolio=port.st, initDate=initDate)   initPortf(port.stsd, symbols=symbols, initDate=initDate)
initAcct(port.stsd, portfolios=port.stsd, initDate=initDate,, initEq=initEq)
initOrders(portfolio=port.stsd, initDate=initDate)   print("setup completed")   # Process the indicators and generate trades
start_t<-Sys.time()
out<-try(applyStrategy(strategy=stratCUD , portfolios=port.st ) )
end_t<-Sys.time()
print("Strategy Loop:")
print(end_t-start_t)   # Process buy and hold strategy
start_t<-Sys.time()
out<-try(applyStrategy(strategy=stratCUDsd , portfolios=port.stsd ) )
end_t<-Sys.time()
print("Strategy Loop:")
print(end_t-start_t)   start_t<-Sys.time()
updatePortf(Portfolio=port.st,Dates=paste('::',as.Date(Sys.time()),sep=''))
updatePortf(Portfolio=port.stsd,Dates=paste('::',as.Date(Sys.time()),sep=''))
end_t<-Sys.time()
print("trade blotter portfolio update:")
print(end_t-start_t)   # hack for new quantmod graphics, remove later
themelist<-chart_theme()
themelist$col$up.col<-'lightgreen'
themelist$col$dn.col<-'pink'   for(symbol in symbols){
#	dev.new()
#	chart.Posn(Portfolio=port.stsd,Symbol=symbol,theme=themelist)
#	#add the CUD indicator to the bottom of the chart
#	plot(add_TA(CUDsd(get(symbol)[,4],nsd=num_periods_sd,nsum=num_periods_sum)))
#	plot(add_TA(CUD(get(symbol)[,4],n=num_periods),on=4,col="red"))
	dev.new()
	chart.Reconcile(port.stsd,port.st,symbol)
	plot(add_TA(CUDsd(get(symbol)[,4],nsd=num_periods_sd,nsum=num_periods_sum)))
	plot(add_TA(CUD(get(symbol)[,4],n=num_periods),on=5,col="red"))   }   tradeStats(port.st)
tradeStats(port.stsd)
```
