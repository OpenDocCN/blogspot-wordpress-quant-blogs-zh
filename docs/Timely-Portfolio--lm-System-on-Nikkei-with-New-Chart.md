<!--yml

分类：未分类

日期：2024-05-18 15:12:30

-->

# 及时投资组合：新的图表下，日经 225 上的 LM 系统

> 来源：[`timelyportfolio.blogspot.com/2011/08/lm-system-on-nikkei-with-new-chart.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/08/lm-system-on-nikkei-with-new-chart.html#0001-01-01)

```
#third version
#add another neat chart for visualization
#got idea from zoo-overplot demo   #second version
#this one actually has an additional mean reverting element
#for markets that have moved down so long entry is quicker
require(PerformanceAnalytics)
require(quantmod)   #set this up to get either FRED or Yahoo!Finance
#getSymbols("N225",src="FRED")
getSymbols("^N225",from="1896-01-01",to=Sys.Date())   N225 <- to.weekly(N225)[,4]
N225mean <- runMean(N225,n=30)
#index(N225) <- as.Date(index(N225))    width = 10
for (i in (width+1):NROW(N225)) {
	linmod <- lm(N225[((i-width):i),1]~index(N225[((i-width):i)]))
	ifelse(i==width+1,signal <- coredata(linmod$residuals[length(linmod$residuals)]),
		signal <- rbind(signal,coredata(linmod$residuals[length(linmod$residuals)])))
	ifelse(i==width+1,signal2 <- coredata(linmod$coefficients[2]),
		signal2 <- rbind(signal2,coredata(linmod$coefficients[2])))
	ifelse(i==width+1,signal3 <- cor(linmod$fitted.values,N225[((i-width):i),1]),
		signal3 <- rbind(signal3,cor(linmod$fitted.values,N225[((i-width):i),1])))
}   signal <- as.xts(signal,order.by=index(N225[(width+1):NROW(N225)]))
signal2 <- as.xts(signal2,order.by=index(N225[(width+1):NROW(N225)]))
signal3 <- as.xts(signal3,order.by=index(N225[(width+1):NROW(N225)]))
signal4 <- ifelse(N225 > N225mean,1,0)   price_ret_signal <- merge(N225,lag(signal,k=1),
	lag(signal2,k=1),
	lag(signal3,k=1),
	lag(signal4,k=1),
	lag(ROC(N225,type="discrete",n=15),k=1),
	ROC(N225,type="discrete",n=1))
	price_ret_signal[,2] <- price_ret_signal[,2]/price_ret_signal[,1]
	price_ret_signal[,3] <- price_ret_signal[,3]/price_ret_signal[,1]
ret <- ifelse((price_ret_signal[,5] == 1) | (price_ret_signal[,5] == 0  &
 	runMean(price_ret_signal[,3],n=50) > 0 & runMean(price_ret_signal[,2],n=10) < 0 ),
	1, 0) * price_ret_signal[,7]
retCompare <- merge(ret, price_ret_signal[,7])
colnames(retCompare) <- c("Linear System", "BuyHold")
#jpeg(filename="performance summary.jpg",
#	quality=100,width=6.25, height = 8,  units="in",res=96)
charts.PerformanceSummary(retCompare,ylog=TRUE,cex.legend=1.2,
	colorset=c("black","gray70"),main="N225 System Return Comparison")
#dev.off()
require(ggplot2)
df <- as.data.frame(na.omit(merge(price_ret_signal[,5],price_ret_signal[,7])))
colnames(df) <- c("signal_avg","return")
#jpeg(filename="boxplot by average.jpg",
#	quality=100,width=6.25, height = 8,  units="in",res=96)
ggplot(df,aes(x=factor(signal_avg),y=return)) + geom_boxplot()
#dev.off()
df2 <- as.data.frame(na.omit(merge(ifelse((price_ret_signal[,5] == 0  &
 	runMean(price_ret_signal[,3],n=50) > 0 & runSum(price_ret_signal[,2],n=10) < 0 ),
	1, 0),price_ret_signal[,7])))
colnames(df2) <- c("signal_other","return")
#jpeg(filename="boxplot by other signal.jpg",
#	quality=100,width=6.25, height = 8,  units="in",res=96)
ggplot(df2,aes(x=factor(signal_other),y=return)) + geom_boxplot()
#dev.off()
df3 <- as.data.frame(na.omit(merge(ifelse((price_ret_signal[,5] == 1) |	(price_ret_signal[,5] == 0  & 
	runMean(price_ret_signal[,3],n=50) > 0 & runMean(price_ret_signal[,2],n=10) < 0 ),
	1, 0),price_ret_signal[,7])))
colnames(df3) <- c("signals_all","return")
#jpeg(filename="boxplot by long signal.jpg",
#	quality=100,width=6.25, height = 8,  units="in",res=96)
ggplot(df3,aes(x=factor(signals_all),y=return)) + geom_boxplot()
#dev.off()
#jpeg(filename="text plot of return and risk.jpg",
	quality=100,width=6.25, height = 6.25,  units="in",res=96)
textplot(rbind(table.AnnualizedReturns(retCompare),
	table.DownsideRisk(retCompare)[c(1:3,7,11),]))
#dev.off()   #eliminate NA at start of return series
retCompare[is.na(retCompare)] <- 0
price_system <- merge(N225,ifelse((price_ret_signal[,5] == 1) |
	(price_ret_signal[,5] == 0  & 
	runMean(price_ret_signal[,3],n=50) > 0 &
	runMean(price_ret_signal[,2],n=10) < 0 ),
	NA, 1),coredata(N225)[width+50]*cumprod(retCompare[,1]+1))
price_system[,2] <- price_system[,1]*price_system[,2]
colnames(price_system) <- c("In","Out","System")   #jpeg(filename="chartSeries with colored entry and exit.jpg",
#	quality=100,width=6.25, height = 6.25,  units="in",res=96)
chartSeries(price_system$System,theme="white",log=TRUE,up.col="black",
	yrange=c(min(price_system[,c(1,3)]),max(price_system[,c(1,3)])),
	TA="addTA(price_system$In,on=1,col=3);
	addTA(price_system$Out,on=1,col=2)",
	name="N225 Linear Model System")
#dev.off()
```
