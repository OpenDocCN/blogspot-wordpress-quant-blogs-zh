<!--yml

类别：未分类

日期：2024-05-18 15:15:11

-->

# 及时投资组合：构建量化策略的基础

> 来源：[`timelyportfolio.blogspot.com/2011/06/quantstrat-to-build-on.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/06/quantstrat-to-build-on.html#0001-01-01)

```
#thanks so much to the developers of quantstrat
#99% of this code comes from the demos in the quantstrat package
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
try(rm("order_book.CUD",pos=.strategy),silent=TRUE)
try(rm("account.CUD","portfolio.CUD",pos=.blotter),silent=TRUE)
try(rm("account.st","portfolio.st","stock.str","stratCUD","initDate","initEq",'start_t','end_t'),silent=TRUE)   
```

```
# Initialize a strategy object
stratCUD <- strategy("CUD")   
```

```
# Add an indicator
stratCUD <- add.indicator(strategy = stratCUD, name = "CUD", arguments = list(price = quote(Cl(mktdata)),n=20), label="CUD")   
```

```
# enter when CUD > 0
stratCUD <- add.signal(strategy = stratCUD, name="sigThreshold",arguments = list(threshold=-0.5, column="CUD",relationship="gt", cross=TRUE),label="CUD.gteq.0")
# exit when CUD < 0
stratCUD <- add.signal(strategy = stratCUD, name="sigThreshold",arguments = list(threshold=-0.5, column="CUD",relationship="lt",cross=TRUE),label="CUD.lt.0")   
```

```
stratCUD <- add.rule(strategy = stratCUD, name='ruleSignal', arguments = list(sigcol="CUD.gteq.0", sigval=TRUE, orderqty=1000, ordertype='market', orderside='long', pricemethod='market', replace=FALSE), type='enter', path.dep=TRUE)
stratCUD <- add.rule(strategy = stratCUD, name='ruleSignal', arguments = list(sigcol="CUD.lt.0", sigval=TRUE, orderqty='all', ordertype='market', orderside='long', pricemethod='market', replace=FALSE), type='exit', path.dep=TRUE)       
```

```
currency("USD")
symbol = "GSPC"
stock(symbol, currency="USD",multiplier=1)
#use paste with ^ to get index data
getSymbols(paste("^",symbol,sep=""),adjust=T,from="1900-12-31")
#I use weekly but comment this out if you want to use daily
GSPC<-to.weekly(GSPC)     
```

```
initDate='1950-12-31'
initEq=100000
port.st<-'CUD' #use a string here for easier changing of parameters and re-trying   
```

```
initPortf(port.st, symbols=symbol, initDate=initDate)
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
print(end_t-start_t)     
```

```
start_t<-Sys.time()
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
chart.Posn(Portfolio=port.st,Symbol=symbol,theme=themelist,log=TRUE)
```
