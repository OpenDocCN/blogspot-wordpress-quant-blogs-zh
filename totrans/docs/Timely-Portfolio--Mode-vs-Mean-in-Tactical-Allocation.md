<!--yml
category: 未分类
date: 2024-05-18 15:12:01
-->

# Timely Portfolio: Mode vs Mean in Tactical Allocation

> 来源：[http://timelyportfolio.blogspot.com/2011/08/mode-vs-mean-in-tactical-allocation.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/08/mode-vs-mean-in-tactical-allocation.html#0001-01-01)

```
require(quantmod)
require(modeest)
require(PerformanceAnalytics)   start = "1990-12-31"
end = Sys.Date()   #use Vanguard funds as proxy for asset classes
#due to Vanguard fees for early redemption
#these funds not appropriate for Tactical system
tckrs <- c("VFINX","VEIEX","VGSTX","VBMFX")
getSymbols(tckrs, from=start, to=end, adjust=TRUE)
for (i in 1:length(tckrs)) {
	assign(tckrs[i],to.monthly(get(tckrs[i]))[,4])
}   funds <- na.omit(merge(VFINX[,1],VEIEX[,1],VGSTX[,1],VBMFX[,1]))
#get dates to include day so format is YYYY-MM-DD
index(funds) <- as.Date(index(funds))
colnames(funds) <- tckrs   #get 1 month change
funds.roc <- ROC(funds,type="discrete",n=1)
#add a balanced benchmark
#20% of each equity fund for 60% total equities
#40% of US bonds
funds.roc <- merge(funds.roc,
	0.2*funds.roc[,1]+0.2*funds.roc[,2]+0.2*funds.roc[,3]+0.4*funds.roc[,4])
funds.roc[1,5] <- 0
colnames(funds.roc) <- c(colnames(funds),"Balanced")   #combine all the funds into one xts
funds <- merge(funds,cumprod(1+funds.roc[,5]))
#charts.PerformanceSummary(funds.roc,
#	main="Vanguard Funds for US, Emerging, Intl Stocks and US Bonds
#	with a 60/40 Balanced Allocation")   #set width to be 10 months similar to Mebane Faber 10 month moving average
width = 10
#set up system.signal with same number of columns and rows as funds
system.signal <- funds
#loop through each column since I could not use apply with mode calculation
for (m in 1:NCOL(system.signal)) {
	#another for loop to do the rolling mode since it also does not work with apply
	for (n in width:NROW(system.signal[,m])) {
		md <- mlv(funds[(n-width):n,m], method = "lientz", bw=0.4)
		ifelse(n==width,
			md.hist <- as.numeric(md[1]),
			md.hist <- rbind(md.hist,as.numeric(md[1])))
	}
	#make into nice xts
	md.xts <- as.xts(as.data.frame(md.hist),
		order.by=index(system.signal[(width):NROW(system.signal)]))
	#put rolling modes into system.signal
	system.signal[(width):NROW(system.signal),m] <- md.hist
}   #jpeg(filename="mode chart.jpg",
#	quality=100,width=6.25, height = 6.25,  units="in",res=96)
plot.zoo(system.signal,main="Modes (lientz) of Funds",nc=1,
	col=c("gray70","steelblue4","darkolivegreen4","goldenrod","purple"))
#dev.off()   #difficult way to get 1 for in and 0 for out
#but the ifelse gave me an index increasing order error
#will use apply instead
system.signal <- funds > system.signal
system.signal[,1:length(tckrs)] <- apply(system.signal[,1:length(tckrs)],MARGIN=2,FUN=as.numeric)
ret.signal <- lag(system.signal,k=1) * funds.roc[,1:5]
ret.compare <- merge(funds.roc[,4],
	0.2*ret.signal[,1]+0.2*ret.signal[,2]+0.2*ret.signal[,3]+0.4*ret.signal[,4],
	ret.signal[,5],
	funds.roc[,5])
colnames(ret.compare) <- c("VBMFX.Bonds","ModeSystem","ModeOnBalanced","Balanced")   #jpeg(filename="signal chart.jpg",
#	quality=100,width=6.25, height = 6.25,  units="in",res=96)
plot.zoo(system.signal,main="Signals (hsm) of Funds",nc=1,
	col=c("gray70","steelblue4","darkolivegreen4","goldenrod","purple"))
#dev.off()   #jpeg(filename="performance summary no average.jpg",
#	quality=100,width=6.25, height = 6.25,  units="in",res=96)
charts.PerformanceSummary(ret.compare,ylog=TRUE,
	main="Performance of Tactical Approaches
	with Balanced Benchmark",
	colorset=c("gray70","steelblue4","darkolivegreen4","goldenrod","purple"),
	cex.legend=1.2,lwd=2)
#dev.off()     #now let's compare to Mebane Faber 10-month moving average strategy
#will do in 1 line since there are multiple examples of how
#to implement this in R
ret.average <- lag(as.xts(apply(
	funds > apply(funds[,1:5],MARGIN=2,FUN=runMean,10),MARGIN=2,as.numeric),order.by=index(funds)),k=1) * funds.roc
ret.compare <- merge(ret.compare,
	0.2*ret.average[,1]+0.2*ret.average[,2]+0.2*ret.average[,3]+0.4*ret.average[,4])
colnames(ret.compare) <- c(colnames(ret.compare)[1:(NCOL(ret.compare)-1)],"Faber10moAvg")   #jpeg(filename="performance summary with Faber average.jpg",
#	quality=100,width=6.25, height = 6.25,  units="in",res=96)
charts.PerformanceSummary(ret.compare,ylog=TRUE,
	main="Performance of Tactical Approaches
	with Balanced Benchmark and Mebane Faber 10mo Mov Avg",
	colorset=c("gray70","steelblue4","darkolivegreen4","goldenrod","purple"),
	cex.legend=1.2,lwd=2)
#dev.off()
```