<!--yml

category: 未分类

date: 2024-05-18 15:14:06

-->

# Timely Portfolio: Hurst as Relative Strength

> 来源：[`timelyportfolio.blogspot.com/2011/06/hurst-as-relative-strength.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/06/hurst-as-relative-strength.html#0001-01-01)

```
#check Hurst exponent system as a potential relative strength signal
#this code is ugly and not very flexible
#I will continue to refine   require(quantmod)
require(PerformanceAnalytics)
require(FGN)   #sort of random mix for additional testing
indexes<-c("GSPC","GDAXI","N225")
getSymbols(paste("^",indexes,sep=""),
	from="1900-01-01",to=format(Sys.Date(),"%Y-%m-%d"))
for (i in 1:length(indexes)) {
	#set monthly index to first day of the month
	assign(indexes[i],to.monthly(get(indexes[i]))[,4])
	#has to be a cleaner way than this to set the index
	assign(indexes[i],as.xts(coredata(get(indexes[i])),
		order.by=as.Date(index(get(indexes[i])))))
}
#get monthly changes
retGSPC<-ROC(GSPC,n=1,type="discrete")
retGDAXI<-ROC(GDAXI,n=1,type="discrete")
retN225<-ROC(N225,n=1,type="discrete")
index(retGSPC) <- as.Date(index(retGSPC))
index(retGDAXI) <- as.Date(index(retGDAXI))
index(retN225) <- as.Date(index(retN225))   hurstKGSPC <- apply.rolling(retGSPC, FUN="HurstK", width = 12)
hurstKGDAXI <- apply.rolling(retGDAXI, FUN="HurstK", width = 12)
hurstKN225 <- apply.rolling(retN225, FUN="HurstK", width = 12)   serialcorrGSPC <- runCor(cbind(coredata(retGSPC)),cbind(index(retGSPC)),n=12)
serialcorrGDAXI <- runCor(cbind(coredata(retGDAXI)),cbind(index(retGDAXI)),n=12)
serialcorrN225 <- runCor(cbind(coredata(retN225)),cbind(index(retN225)),n=12)
serialcorrGSPC <- as.xts(serialcorrGSPC,order.by=index(retGSPC))
serialcorrGDAXI <- as.xts(serialcorrGDAXI,order.by=index(retGDAXI))
serialcorrN225 <- as.xts(serialcorrN225,order.by=index(retN225))   autoregGSPC <- runCor(retGSPC,lag(retGSPC,k=1),n=12)
autoregGDAXI <- runCor(retGDAXI,lag(retGDAXI,k=1),n=12)
autoregN225 <- runCor(retN225,lag(retN225,k=1),n=12)   signalUpTrendGSPC <- runMean(hurstKGSPC+serialcorrGSPC+autoregGSPC,n=6) +
	(GSPC/runMean(GSPC,n=12)-1)*10
signalUpTrendGDAXI <- runMean(hurstKGDAXI+serialcorrGDAXI+autoregGDAXI,n=6) +
	(GDAXI/runMean(GDAXI,n=12)-1)*10
signalUpTrendN225 <- runMean(hurstKN225+serialcorrN225+autoregN225,n=6) +
	(N225/runMean(N225,n=12)-1)*10   #merge returns and lagged signal into one xts for evaluation
ret_signals <- merge(na.omit(merge(retGSPC,retGDAXI,retN225)),
	lag(na.omit(merge(signalUpTrendGSPC,signalUpTrendGDAXI,signalUpTrendN225)),k=1))   #get return from the strongest Hurst exponent
retSys <- ifelse(ret_signals[,4]>ret_signals[,5]&ret_signals[,4]>ret_signals[,6]&ret_signals[,4]>1&(ret_signals[,5]>0.75|ret_signals[,6]>0.75),1,0)*ret_signals[,1]+
	ifelse(ret_signals[,5]>ret_signals[,4]&ret_signals[,5]>ret_signals[,6]&ret_signals[,5]>1&(ret_signals[,4]>0.75|ret_signals[,6]>0.75),1,0)*ret_signals[,2]+
	ifelse(ret_signals[,6]>ret_signals[,4]&ret_signals[,6]>ret_signals[,5]&ret_signals[,6]>1&(ret_signals[,4]>0.75|ret_signals[,5]>0.75),1,0)*ret_signals[,3]   #fill NAs from beginnning periods with no signal with 0
retSys[is.na(retSys)] <- 0   retCompare <- merge(retSys,ret_signals[,1:3])
colnames(retCompare) <- c("Hurst RS System","SP500","DAX","N225")
#jpeg(filename="HurstRS.jpg",quality=100,width=6.25, height = 5, 
#	units="in",res=96) 
charts.PerformanceSummary(retCompare[19:NROW(retCompare),],ylog=TRUE,cex.legend=1.25,
	colorset=c("cadetblue","darkolivegreen3","purple","gray70"))
#dev.off()     #for some risk return comparison
#jpeg(filename="HurstRSRiskReturn.jpg",quality=100,width=6.25, height = 5, 
#	units="in",res=96) 
chart.RiskReturnScatter(retCompare[19:NROW(retCompare),],
	main="Risk Return of Hurst RS System and Indexes")
#dev.off()   #for some ggplot2 risk bar charts
require(ggplot2)
#jpeg(filename="HurstRSRisk.jpg",quality=100,width=6.25, height = 5, 
#	units="in",res=96) 
downsideTable<-melt(cbind(rownames(table.DownsideRisk(retCompare)),table.DownsideRisk(retCompare)))
colnames(downsideTable)<-c("Statistic","Portfolio","Value")
ggplot(downsideTable, stat="identity", aes(x=Statistic,y=Value,fill=Portfolio)) +
	geom_bar(position="dodge") + coord_flip()
#dev.off()
```
