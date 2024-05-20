<!--yml
category: 未分类
date: 2024-05-18 15:12:39
-->

# Timely Portfolio: System Failure-Maybe it Will Help

> 来源：[http://timelyportfolio.blogspot.com/2011/08/system-failure-maybe-it-will-help.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/08/system-failure-maybe-it-will-help.html#0001-01-01)

```
require(PerformanceAnalytics)
require(quantmod)   #set this up to get either FRED or Yahoo!Finance
#getSymbols("GSPC",src="FRED")
getSymbols("^GSPC",from="1896-01-01",to=Sys.Date())     GSPC <- to.weekly(GSPC)[,4]
#GSPCmean <- runMean(GSPC,n=20)
#index(GSPC) <- as.Date(index(GSPC))   width = 25
for (i in (width+1):NROW(GSPC)) {
	linmod <- lm(GSPC[((i-width):i),1]~index(GSPC[((i-width):i)]))
	ifelse(i==width+1,signal <- coredata(linmod$residuals[length(linmod$residuals)]),
		signal <- rbind(signal,coredata(linmod$residuals[length(linmod$residuals)])))
	ifelse(i==width+1,signal2 <- coredata(linmod$coefficients[2]),
		signal2 <- rbind(signal2,coredata(linmod$coefficients[2])))
	ifelse(i==width+1,signal3 <- cor(linmod$fitted.values,GSPC[((i-width):i),1]),
		signal3 <- rbind(signal3,cor(linmod$fitted.values,GSPC[((i-width):i),1])))
}
signal <- as.xts(signal,order.by=index(GSPC[(width+1):NROW(GSPC)]))
signal2 <- as.xts(signal2,order.by=index(GSPC[(width+1):NROW(GSPC)]))
signal3 <- as.xts(signal3,order.by=index(GSPC[(width+1):NROW(GSPC)]))   price_ret_signal <- merge(GSPC,lag(signal,k=1),
	lag(signal2,k=1),lag(signal3,k=1),
	ROC(GSPC,type="discrete",n=1))
price_ret_signal[,2] <- price_ret_signal[,2]/price_ret_signal[,1]
price_ret_signal[,3] <- price_ret_signal[,3]/price_ret_signal[,1]   #ret <- ifelse((runMin(price_ret_signal[,3],n=10) >= 0  &
#	runSum(price_ret_signal[,2],n=30) >= 0.0) | 
#	(runMin(price_ret_signal[,3],30) < 0 & 
#	runSum(price_ret_signal[,2],n=50) >= 0.02),
#	 1, 0) * price_ret_signal[,5]
#ret <- ifelse(runSum(price_ret_signal[,3],n=10) >= 0, 1, 0) * price_ret_signal[,5]   ret <- ifelse((runMean(price_ret_signal[,3],n=5) > 0 & 
	runMean(price_ret_signal[,4],n=5) > 0.25),
	1, 0) * price_ret_signal[,5]   retCompare <- merge(ret, price_ret_signal[,5])
colnames(retCompare) <- c("Linear System", "BuyHold")
charts.PerformanceSummary(retCompare,ylog=TRUE,cex.legend=1.2,
	colorset=c("black","gray70"),main="GSPC System Return Comparison")
```