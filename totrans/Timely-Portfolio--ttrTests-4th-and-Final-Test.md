<!--yml
category: 未分类
date: 2024-05-18 15:11:23
-->

# Timely Portfolio: ttrTests 4th and Final Test

> 来源：[http://timelyportfolio.blogspot.com/2011/10/ttrtests-4th-and-final-test.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/10/ttrtests-4th-and-final-test.html#0001-01-01)

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
test_price <- as.vector(get(tckrs[i])[,4])   #run subperiods and paramPersist to test for luck across subperiods
#"asks whether or not good choices of parameters"
#"were robust across different time periods"
#chose 6 since data is from 1950 will approximate by decade
subper <- subperiods(x=test_price, periods = 6, ttr = CUD,
	start = 20, nSteps = 30, stepSize = 10, restrict = FALSE,
	burn = 0, short = FALSE, condition = NULL,
	silent = TRUE, TC = 0.001, loud = TRUE, alpha = 0.025,
	file = "", benchmark = "hold")   #make output slightly more usable with some naming
#believe I got this right
names(subper[[2]]) <- "obs.correlation"
#while we are in a nasty for loop; grab some data also
for (j in 3:length(subper)) {
	names(subper[[j]]) <- paste(c("excess.return","z.score","adj.excess.return",
		"Sharpe.ratio","best","best.repeat","best.adjusted",
		paste("tested.parameters",c(1:(NROW(subper[[j]])-7)),sep="")))
		# add this if desired		".subper",j-2, sep="")
	ifelse(j==3, excess.df <- cbind(rep(j-2,length(subper[[j]]$tested.parameters)),
		subper[[j]]$tested.parameters,
		subper[[j]]$excess.return),
		excess.df <- rbind(excess.df,
		cbind(rep(j-2,length(subper[[j]]$tested.parameters)),
		subper[[j]]$tested.parameters,
		subper[[j]]$excess.return)))
}
excess.df <- as.data.frame(excess.df)
colnames(excess.df) <- c("subperiod","parameter","excess.ret")   #run boxplot of excess returns by parameter
jpeg(filename="boxplot.jpg",
	quality=100,width=6.25, height = 6.25,  units="in",res=96)
boxplot(excess.df$excess.ret~excess.df$parameter, 
	xlab="Parameter", ylab="Excess Return",
	main="Boxplot of Excess Returns by Parameter")
dev.off()   #jpeg(filename="strip chart.jpg",
#	quality=100,width=6.25, height = 6.25,  units="in",res=96)
stripchart(excess.df$excess.ret~excess.df$parameter, pch=19,
	xlab="Parameter", ylab="Excess Return", vertical=TRUE,
	col=topo.colors(NROW(subper[[j]]$tested.parameters)),
	main="Stripchart of Excess Returns by Parameter")
#dev.off()     #and my favorite of all
#"tests if the persistence measure from subperiods()"
#"is statistically significant"
#this takes the longest (about 28 minutes on my i7 laptop)
#if you want to play 
#change periods to 2 or bsamples to 10 to speed time
parpersist <- paramPersist(x=test_price, ttr = CUD, periods=6,
	start = 20, nSteps = 30, stepSize = 10,
	bSamples=100,
	restrict = FALSE, burn = 0, short = FALSE, condition = NULL,
	silent = TRUE, TC = 0.001, loud = TRUE, alpha = 0.025,
	file = "")
names(parpersist) <- c("act.corr","obs.corr.samples","p.value")   #jpeg(filename="paramPersist correlations.jpg",
#	quality=100,width=6.25, height = 6.25,  units="in",res=96)
plot(parpersist$obs.corr.samples,ylab="Correlation",xlab="Sample",
	main="paramPersist for CUD")
abline(h=parpersist$act.corr,col="darkslateblue")
text(0,parpersist$act.corr, "actual", col = "darkslateblue", adj = c(0, -.1))
#dev.off()   #make output slightly more usable with some naming
#believe I got this right
names(snoop) <- c("details","V1","V2",
	"V3","p1.for.l","p2.for.c","p3.for.u")   #jpeg(filename="dataSnoop values.jpg",
	quality=100,width=6.25, height = 6.25,  units="in",res=96)
plot(snoop$V3,
	type="l", col=2,
	main="ttrTests dataSnoop V1,V2,and V3 on CUD",
	xlab="Bootstrap Sample", ylab="Values")
points(snoop$V2, type="l", col=3)
points(snoop$V1, col=4)
legend("topright",legend=c("V1","V2","V3"),col=c(4,3,2),pch=19,lty=1)
#dev.off()
```