<!--yml
category: 未分类
date: 2024-05-18 15:15:07
-->

# Timely Portfolio: A Quantstrat to Build on Part 2

> 来源：[http://timelyportfolio.blogspot.com/2011/06/quantstrat-to-build-on-part-2.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/06/quantstrat-to-build-on-part-2.html#0001-01-01)

```
#thanks so much to the developers of quantstrat
#99% of this code comes from the demos in the quantstrat package   
```

```
#in this I make 4 changes to that posted 6/2/2011
#1.Add another index GDAXI (German Dax) for additional testing;
# for now use USD but see faberMC demo for currency fun;
# I'll save more for out of sample testing
#2.Change the number of periods (in this case weeks) to 50 from 20
# so we have less signals and enjoy life more.  I also added this as
# variable early in the code, so we only have to change once to apply
# across the system and charts
#3.Change the gt(>) –0.5 that I hacked originally to the more correct
# gte (>=) 0 relationship provided by quantstrat
#4.Added the CUD indicator to the chart.Posn with add_TA
# (note add_TA works and TA=”addTA..” does not) and removed
# the log=TRUE option which does not work   
```

```
#now let's define our silly countupdown function
CUD <- function(price,n) {
	#CUD takes the n-period sum of 1 (up days) and -1 (down days)
	temp<-runSum(ifelse(ROC(price,1,type="discrete") > 0,1,-1),n)
	colnames(temp) <- "CUD"
	temp
}   
```

```
require(quantstrat)
```

```
try(rm("order_book.CUD",pos=.strategy),silent=TRUE)
try(rm("account.CUD","portfolio.CUD",pos=.blotter),silent=TRUE)
try(rm("port.st","symbols","symbol","stratCUD","initDate","initEq",
	'start_t','end_t','num_periods'),silent=TRUE)   
```

```
#specify this for the rolling periods to use for our signal
num_periods=50   
```

```
# Initialize a strategy object
stratCUD <- strategy("CUD")  
```

```
# Add an indicator
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
	arguments = list(sigcol="CUD.gte.0", sigval=TRUE, orderqty=1000, ordertype='market',
	 orderside='long', pricemethod='market', replace=FALSE), type='enter', path.dep=TRUE)
stratCUD <- add.rule(strategy = stratCUD, name='ruleSignal', 
	arguments = list(sigcol="CUD.lt.0", sigval=TRUE, orderqty='all',
	 ordertype='market', orderside='long', pricemethod='market', replace=FALSE),
	 type='exit', path.dep=TRUE)   currency("USD")
symbols = c("GSPC","GDAXI")
for (symbol in symbols) {
	stock(symbol, currency="USD",multiplier=1)
	#use paste with ^ to get index data
	getSymbols(paste("^",symbol,sep=""),adjust=T,from="1900-12-31")
	assign(symbol,to.weekly(get(symbol)))
}   
```

```
initDate='1950-12-31'
initEq=100000
port.st<-'CUD' 
```

```
#use a string here for easier changing of parameters and re-trying   
```

```
initPortf(port.st, symbols=symbols, initDate=initDate)
initAcct(port.st, portfolios=port.st, initDate=initDate)
initOrders(portfolio=port.st, initDate=initDate)   
```

```
print("setup completed")   
```

```
# Process the indicators and generate trades
start_t<-Sys.time()
out<-try(applyStrategy(strategy=stratCUD , portfolios=port.st ) )
end_t<-Sys.time()
print("Strategy Loop:")
print(end_t-start_t)   start_t<-Sys.time()
updatePortf(Portfolio=port.st,Dates=paste('::',as.Date(Sys.time()),sep=''))
end_t<-Sys.time()
print("trade blotter portfolio update:")
print(end_t-start_t)   
```

```
# hack for new quantmod graphics, remove later
themelist<-chart_theme()
themelist$col$up.col<-'lightgreen'
themelist$col$dn.col<-'pink'   
```

```
for(symbol in symbols){
	dev.new()
	chart.Posn(Portfolio=port.st,Symbol=symbol,theme=themelist)
	#add the CUD indicator to the bottom of the chart
	plot(add_TA(CUD(get(symbol)[,4],n=num_periods)))
}
```