<!--yml

category: 未分类

date: 2024-05-18 15:12:26

-->

# Timely Portfolio: ttrTests Experimentation

> 来源：[`timelyportfolio.blogspot.com/2011/08/ttrtests-experimentation.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/08/ttrtests-experimentation.html#0001-01-01)

```
#let's define our silly countupdown function
#as a sample of a custom ttr rule
CUD <- function(x,params=50,...) {
	#CUD takes the n-period sum of 1 (up days) and -1 (down days)
	temp <- ifelse(runSum(ifelse(ROC(x,1,type="discrete") > 0,1,-1),params)>=0,1,0)
	#replace NA with 0 at beginning of period
	temp[is.na(temp)] <- 0
	temp
}   require(ttrTests)
require(quantmod)
require(lattice)
require(reshape2)
require(PerformanceAnalytics)   #defaults functions is overridden by ggplot2 and plyr if loaded
#and will cause problems if you want to use ttrTests concurrently   tckrs <- c("GSPC","RUT","N225","GDAXI","DJUBS")   for (i in 1:length(tckrs)) {
	getSymbols(paste("^",tckrs[i],sep=""),from="1896-01-01",to=Sys.Date())
	test_price <- as.vector(get(tckrs[i])[,4])
	#do parameter tests but plot=FALSE
	#we will plot later
	#if you want plot=TRUE make sure you add dev.new() here
	param_results <- paramStats(x=test_price, ttr = CUD, start = 20, nSteps = 30, stepSize = 10,
		restrict = FALSE, burn = 0, short = FALSE, condition = NULL,
		silent = TRUE, TC = 0.001, loud = TRUE, plot = FALSE, alpha = 0.025,
		begin = 1, percent = 1, file = "", benchmark = "hold")
	#get excess returns and add to matrix
	ifelse(i==1,param_all <- param_results[[1]],
		param_all <- cbind(param_all,param_results[[1]]))
	#get best parameter and add to matrix
	ifelse(i==1,param_best <- param_results[[5]],
		param_best <- rbind(param_best,param_results[[5]]))
}
rownames(param_best) <- tckrs
print(param_best)   param_all <- cbind(param_results[[8]],param_all)
#fix rownames and colnames for param_all
colnames(param_all) <- c("parameters",tckrs)   df <- as.data.frame(param_all)
df.melt <- melt(df,id.vars=1)
colnames(df.melt) <- c("parameters","index","excessreturn")
param_plot <- xyplot(excessreturn~parameters,group=index,data=df.melt,
	auto.key=TRUE,type="l",main="Excess Returns by Parameter")
#jpeg(filename="excess return by parameter.jpg",
	quality=100,width=6.25, height = 6.25,  units="in",res=96)
print(param_plot)
#want to add points for max but unsure how currently
#df.melt[which(df.melt$parameters==param_best[1,] & df.melt$index==rownames(param_best)[1] ),3]
dev.off()   #get performance summary for the best parameters
for (i in 1:length(tckrs)) {
	dev.new()
	#jpeg(filename=paste(tckrs[i],"performance summary.jpg",sep=""),
	#	quality=100,width=6.25, height = 6.25,  units="in",res=96)
	ret <- merge(lag(CUD(get(tckrs[i])[,4],
		coredata(param_best)[1],k=1))*ROC(get(tckrs[i])[,4],type="discrete", n=1),
		ROC(get(tckrs[i])[,4],type="discrete", n=1))
	colnames(ret)<-c(paste(tckrs[i]," CUD System",sep=""),tckrs[i])
	charts.PerformanceSummary(ret,ylog=TRUE)
	#dev.off()
	ret[1,]<-0
	price_system <- merge(get(tckrs[i])[,4],
		lag(CUD(get(tckrs[i])[,4],
		coredata(param_best)[1],k=1))*get(tckrs[i])[,4],
		cumprod(1+ret[,1])*coredata(get(tckrs[i]))[coredata(param_best)[1],4])
	price_system[which(price_system[,2]==0),2] <- NA
	colnames(price_system) <- c("Out","In","System")   dev.new()
	#jpeg(filename=paste(tckrs[i],"entry analysis.jpg",sep=""),
	#	quality=100,width=6.25, height = 6.25,  units="in",res=96)
	chartSeries(price_system$System,theme="white",log=TRUE,up.col="black",
		yrange=c(min(price_system[,c(1,3)]),max(price_system[,c(1,3)])),
		TA="addTA(price_system$Out,on=1,col=2);
		addTA(price_system$In,on=1,col=3)",
		name=paste(tckrs[i]," Linear Model System",sep=""))
	#dev.off()
}
```
