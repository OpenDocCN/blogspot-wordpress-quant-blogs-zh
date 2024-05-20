<!--yml
category: 未分类
date: 2024-05-18 15:12:52
-->

# Timely Portfolio: Crazy RUT

> 来源：[http://timelyportfolio.blogspot.com/2011/07/crazy-rut.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/07/crazy-rut.html#0001-01-01)

```
require(quantmod)
require(PerformanceAnalytics)   getSymbols("^RUT",from="1919-01-01",to=Sys.Date())   RUT <- to.monthly(RUT)[,4]
index(RUT) <- as.Date(index(RUT))   #get 10 month rolling average
avg10 <- runMean(RUT,n=10)   #know I can do this better in R but here is my ugly code
#to calculate 6 month slope of 10 month average
width=6
for (i in 1:(NROW(avg10)-width)) {	
	#get sp500/crb slope
	model <- lm(RUT[i:(i+width),1]~index(RUT[i:(i+width)]))
	ifelse(i==1,avg10slope <- model$coefficients[2],
		avg10slope <- rbind(avg10slope,model$coefficients[2]))
}
#get xts so we can use
avg10slope <- xts(cbind(avg10slope),order.by=index(avg10)[(width+1):NROW(avg10)])   priceSignals <- na.omit(merge(RUT,avg10,avg10slope))   signalUpUp <- ifelse(priceSignals[,1] > priceSignals[,2] & priceSignals[,3] > 0, 1, 0)
signalUpDown <- ifelse(priceSignals[,1] > priceSignals[,2] & priceSignals[,3] < 0, 1, 0)
signalDownUp <- ifelse(priceSignals[,1] < priceSignals[,2] & priceSignals[,3] > 0, 1, 0)
signalDownDown <- ifelse(priceSignals[,1] < priceSignals[,2] & priceSignals[,3] < 0, 1, 0)   retUpUp <- lag(signalUpUp,k=1)* ROC(RUT,type="discrete",n=1)
retUpDown <- lag(signalUpDown,k=1)* ROC(RUT,type="discrete",n=1)
retDownUp <- lag(signalDownUp, k=1) * ROC(RUT,type="discrete",n=1)
retDownDown <- lag(signalDownDown, k=1) * ROC(RUT,type="discrete",n=1)   ret <- merge(retUpUp,retUpDown,retDownUp,retDownDown,ROC(RUT,type="discrete",n=1))
colnames(ret) <- c("UpUp","UpDown","DownUp","DownDown","RUT")   jpeg(filename="performance summary.jpg",quality=100,
	width=6.25, height = 6.25,  units="in",res=96)
charts.PerformanceSummary(ret,ylog=TRUE,
	colorset=c("cadetblue","darkolivegreen3","goldenrod","purple","gray70","black"),
	main="RUT 10 Month Moving Average Strategy Comparisons
	May 1987-Jun 2011")
dev.off()   jpeg(filename="rolling returns.jpg",quality=100,
	width=6.25, height = 6.25,  units="in",res=96)
chart.RollingPerformance(ret,width=36,
	colorset=c("cadetblue","darkolivegreen3","goldenrod","purple","gray70","black"),
	main="RUT 10 Month Moving Average Strategy Comparisons
	36 Month Rolling Return May 1987-Jun 2011")
dev.off()
```