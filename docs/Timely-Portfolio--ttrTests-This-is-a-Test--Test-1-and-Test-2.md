<!--yml

分类：未分类

日期：2024-05-18 15:11:44

-->

# 及时投资组合：ttrTests 这是一个测试--测试 1 和测试 2

> 来源：[`timelyportfolio.blogspot.com/2011/09/ttrtests-this-is-test-test-1-and-test-2.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/09/ttrtests-this-is-test-test-1-and-test-2.html#0001-01-01)

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
#and will cause problems if you want to use ttrTests concurrently   tckrs <- c("GSPC","RUT","N225","GDAXI","DJUBS")   #use 1 or GSPC but adjust however you would like
i=1
getSymbols(paste("^",tckrs[i],sep=""),from="1896-01-01",to=Sys.Date())
test_price <- as.vector(get(tckrs[i])[,4])
#do parameter tests but plot=FALSE
#we will plot later
param_results <- paramStats(x=test_price, ttr = CUD, start = 20, nSteps = 30, stepSize = 10,
	restrict = FALSE, burn = 0, short = FALSE, condition = NULL,
	silent = TRUE, TC = 0.001, loud = TRUE, plot = FALSE, alpha = 0.025,
	begin = 1, percent = 1, file = "", benchmark = "hold")
#make output slightly more usable with some naming
#believe I got this right
names(param_results) <- c("excess.return","z.score","adj.excess.return",
	"Sharpe.ratio","best","best.repeat","best.adjusted",
	paste("tested.parameters",c(1:(NROW(param_results)-7)),sep=""))
#jpeg(filename="excess by parameter.jpg",
	quality=100,width=6.25, height = 6.25,  units="in",res=96)
plot(param_results$excess.return~param_results$tested.parameters1,
	type="l", col="darkgray",
	main="ttrTests Excess Return by Parameter")
abline(v=param_results$best, col="indianred3")
#dev.off()   #let's use the returnStats function to get
#more complete return and distribution info on the best parameter
stats <- returnStats(x=test_price, ttr=CUD, params=param_results$best,
	short=FALSE, TC=0.001, benchmark="hold")
#make output slightly more usable with some naming
#believe I got this right
names(stats) <- c("benchmark.stats","ttr.stats","adj.stats.and.periods",
	"excess.stats","long.stats","short.stats","neutral.stats")
#jpeg(filename="analysis of returns.jpg",
	quality=100,width=6.25, height = 6.25,  units="in",res=96)
barplot(c(stats$long.stats[1],stats$short.stats[1],
	stats$neutral.stats[1],stats$benchmark.stats[1]),
	col=c("darkolivegreen3","indianred3","steelblue3","gray70"),
	names.arg=c("long","short","neutral","benchmark"),
	main="Analysis of Returns from ttrTests")
#dev.off()   #now let's test the best parameter with nullModel
#this tests the parameter with bootstrap resampling
#for significance across one of three criteria
#specified by crit = "sharpe", "return" (excess return),
#or "adjust" (excess adjusted  for trading costs)
nmodel <- nullModel(x=test_price, model="stationaryBootstrap", userParams=4, bSamples=100,
	ttr=CUD, params=param_results$best, short=FALSE, TC=0.001, crit="sharpe",
	benchmark="hold")
#make output slightly more usable with some naming
#believe I got this right
#this is different from documentation but code seems to
#fit with this
names(nmodel) <- c("excess.return","excess.Sharpe.ratio","adj.excess.return","p.value")
#jpeg(filename="excess return by bootstrap.jpg",
	quality=100,width=6.25, height = 6.25,  units="in",res=96)
plot(nmodel$excess.return,type="l",xlab="Bootstrap Sample",
	main="Excess Return for each Bootstrapped Sample")
#add line for excess return from actual ttr performance
abline(h=stats$excess.stats[1], col="indianred3")
#dev.off()   #jpeg(filename="excess adjusted return by bootstrap.jpg",
	quality=100,width=6.25, height = 6.25,  units="in",res=96)
plot(nmodel$adj.excess.return,type="l",col="khaki4",
	main="Excess Adjusted Return for each Bootstrapped Sample")
#add line for excess adjusted from actual ttr performance
abline(h=stats$adj.stats.and.periods[1], col="indianred3")
#dev.off()   #jpeg(filename="excess sharpe ratio by bootstrap.jpg",
	quality=100,width=6.25, height = 6.25,  units="in",res=96)
plot(nmodel$excess.Sharpe.ratio,type="l",lwd=2,xlab="BootstrapSample",col="cadetblue4",
	main="Excess Sharpe Ratio for each Bootstrapped Sample")
#add line for excess sharpe from actual ttr performance
abline(h=stats$ttr.stats[3]-stats$benchmark.stats[3], col="indianred3")
#dev.off()
```
