<!--yml

类别：未分类

日期：2024-05-18 15:13:21

-->

# [及时投资组合：构建量化策略（第六部分）](http://timelyportfolio.blogspot.com/2011/07/quantstrat-to-build-on-part-6.html#0001-01-01)

> 来源：[`timelyportfolio.blogspot.com/2011/07/quantstrat-to-build-on-part-6.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/07/quantstrat-to-build-on-part-6.html#0001-01-01)

```
#thanks so much to the developers of quantstrat
#99% of this code comes from the demos in the quantstrat package   #in this I use osFun to size orders to ending equity
#for a more appropriate comparison to buy hold   #takes longer than I would like but is acceptable
#another way to accomplish testing and reporting
#is use 1 for orderqty and then generate return series
#with this as signal   #however despite extra time I like to see growth in order size
#with performance
#makes a very valid point for drawdown reduction     require(quantstrat)
require(PerformanceAnalytics)   #now let's define our silly countupdown function
CUD <- function(price,n) {
	#CUD takes the n-period sum of 1 (up days) and -1 (down days)
	temp <- runSum(ifelse(ROC(price,1,type="discrete") > 0,1,-1),n)
	colnames(temp) <- "CUD"
	temp
}   BuyHold <- function(price,periodtobuy) {
	#just enter true (1) the period specified as buy and hold
	#for the remainder
	temp <- as.xts(rep(0,NROW(price)),order.by=index(price))
	colnames(temp) <- "BuyHold"
	temp[periodtobuy,1]<-1
	temp
}   osFillErUp <- function (data, timestamp, orderqty, ordertype, orderside, portfolio, symbol, ruletype, ..., orderprice) 
{   #get date in usable xts format
	datePos <- format(timestamp,"%Y-%m-%d")
	#update the portfolio to date of trade rule
	updatePortf(Portfolio=portfolio,Symbol=symbol,Dates=paste('::',datePos,sep=''))
	portf <- getPortfolio(portfolio)
	#get price of symbol for the date of trade rule
	price <- getPrice(get(symbol))[datePos]
	#get amount generated from the last trade
	#best way for me to overcome lack of cumulative p/l for portfolio by symbol
	#all this logic is at the account level
	trades <- getOrderBook(portfolio)[[portfolio]][[symbol]]
	#if first trade, just use order quantity specified
	#if not get order quantity equal to
	#last trade proceeds divided by price of symbol at trade date
	if(NROW(trades)>1) {
		trades <- trades[NROW(trades)]
		endEq <- as.numeric(trades$Order.Qty) * as.numeric(trades$Order.Price)
#		orderqty <- abs(endEq/price)
		orderqty <- abs(floor(endEq/price))
	}
	#return the new orderqty
	osFillErUp <- orderqty
}     try(rm("order_book.CUD",pos=.strategy),silent=TRUE)
try(rm("order_book.BuyHold",pos=.strategy),silent=TRUE)
try(rm("account.CUD","portfolio.CUD",pos=.blotter),silent=TRUE)
try(rm("account.BuyHold","portfolio.BuyHold",pos=.blotter),silent=TRUE)
try(rm("port.st","symbols","symbol","stratCUD","initDate","initEq",
	'start_t','end_t','num_periods'),silent=TRUE)   #specify this for the rolling periods to use for our signal
num_periods=50   # Initialize a strategy object
stratCUD <- strategy("CUD")   # Add an indicator
stratCUD <- add.indicator(strategy = stratCUD, name = "CUD", 
	arguments = list(price = quote(Cl(mktdata)),n=num_periods),
	label="CUD")   # enter when CUD > 0
stratCUD <- add.signal(strategy = stratCUD, name="sigThreshold",
	arguments = list(threshold=0, column="CUD",relationship="gte", cross=TRUE),
	label="CUD.gte.0")
# exit when CUD < 0
stratCUD <- add.signal(strategy = stratCUD, name="sigThreshold",
	arguments = list(threshold=0, column="CUD",relationship="lt",cross=TRUE),
	label="CUD.lt.0")   stratCUD <- add.rule(strategy = stratCUD, name='ruleSignal', 
	arguments = list(sigcol="CUD.gte.0", sigval=TRUE, orderqty=100, ordertype='market',
	 orderside='long', pricemethod='market', replace=FALSE, osFUN='osFillErUp'), type='enter', path.dep=TRUE)
stratCUD <- add.rule(strategy = stratCUD, name='ruleSignal', 
	arguments = list(sigcol="CUD.lt.0", sigval=TRUE, orderqty='all',
	 ordertype='market', orderside='long', pricemethod='market', replace=FALSE),
	 type='exit', path.dep=TRUE)   #Initialize a buy/hold strategy object
stratBuyHold <- strategy("BuyHold")
stratBuyHold <- add.indicator(strategy = stratBuyHold, name = "BuyHold",
	arguments = list(price = quote(Cl(mktdata)),periodtobuy=num_periods),
	label = "BuyHold")
stratBuyHold <- add.rule(strategy=stratBuyHold, name='ruleSignal',
	arguments = list(sigcol="BuyHold",sigval=TRUE,orderqty=100,ordertype='market',
	 orderside='long', pricemethod='market', replace=FALSE), type='enter', path.dep=TRUE)     currency("USD")
symbols = c("GSPC","GDAXI")
for (symbol in symbols) {
	stock(symbol, currency="USD",multiplier=1)
	#use paste with ^ to get index data
	getSymbols(paste("^",symbol,sep=""),adjust=T,from="1900-12-31")
	assign(symbol,to.weekly(get(symbol)))
}   initDate='1949-12-31'
initEq=1000000
port.st<-'CUD' #use a string here for easier changing of parameters and re-trying
port.buyhold <- 'BuyHold'   initPortf(port.st, symbols=symbols, initDate=initDate)
initAcct(port.st, portfolios=port.st, initDate=initDate, initEq=initEq)
initOrders(portfolio=port.st, initDate=initDate)   initPortf(port.buyhold, symbols=symbols, initDate=initDate)
initAcct(port.buyhold, portfolios=port.buyhold, initDate=initDate,, initEq=initEq)
initOrders(portfolio=port.buyhold, initDate=initDate)   print("setup completed")   # Process the indicators and generate trades
start_t<-Sys.time()
out<-try(applyStrategy(strategy=stratCUD , portfolios=port.st ) )
end_t<-Sys.time()
print("Strategy Loop:")
print(end_t-start_t)   # Process buy and hold strategy
start_t<-Sys.time()
out<-try(applyStrategy(strategy=stratBuyHold , portfolios=port.buyhold ) )
end_t<-Sys.time()
print("Strategy Loop:")
print(end_t-start_t)   start_t<-Sys.time()
updatePortf(Portfolio=port.st,Dates=paste('::',as.Date(Sys.time()),sep=''))
updatePortf(Portfolio=port.buyhold,Dates=paste('::',as.Date(Sys.time()),sep=''))
end_t<-Sys.time()
print("trade blotter portfolio update:")
print(end_t-start_t)   # hack for new quantmod graphics, remove later
themelist<-chart_theme()
themelist$col$up.col<-'lightgreen'
themelist$col$dn.col<-'pink'   for(symbol in symbols){
	#dev.new()
	#chart.Posn(Portfolio=port.st,Symbol=symbol,theme=themelist)
	#add the CUD indicator to the bottom of the chart
	#jpeg(filename=paste(symbol," Reconcile.jpg",sep=""),quality=100,
	#	width=6.5, height = 6.5,  units="in",res=96)
	chart.Reconcile(port.buyhold,port.st,symbol)
	plot(add_TA(CUD(get(symbol)[,4],n=num_periods)))
	#dev.off()
}   #tradeStats(port.st)   #backwards way to get returns
#again to bypass account p/l logic
port <- getPortfolio(port.st)
for(symbol in symbols) {
	#get posPL for the symbol in the portfolio
	posPLTable <- port$symbols[[symbol]][["posPL"]]
	#easier this way to get ROC for each day when position is held (Pos.Qty > 0)
	#rets <- lag(ifelse(posPLTable$Pos.Qty>0,1,0),k=1)*ROC(get(symbol)[,4],type="discrete",n=1)
	#the previous commented method is not exactly correct
	#since we can only hold integer positions
	#to account for this difference we can get
	rets <- posPLTable$Gross.Trading.PL/lag(posPLTable$Pos.Value,k=1)
	rets[is.na(rets)] <- 0
	rets[which(rets[,1]==Inf)] <- 0
	rets[which(rets[,1]==-Inf)] <- 0
	retCompare <- merge(rets,ROC(get(symbol)[,4],type="discrete",n=1))
	colnames(retCompare) <- c(paste(symbol," CUD System",sep=""),symbol)
	#jpeg(filename=paste(symbol," Performance.jpeg",sep=""),quality=100,width=6.5, height = 6.5,
	#	units="in",res=96)
	charts.PerformanceSummary(retCompare,ylog=TRUE,
		colorset=c("black","gray70"),
		main = paste(symbol," CUD System and Index 
		Performance Summary",sep=""))
	#dev.off()
	#jpeg(filename=paste(symbol," Capture.jpeg",sep=""),quality=100,width=6.5, height = 6.5,
	#	units="in",res=96)
	chart.CaptureRatios(retCompare[,1],retCompare[,2],
		main = paste(symbol," CUD System and Index 
		Capture Ratios",sep=""))
	#dev.off() 
}
```
