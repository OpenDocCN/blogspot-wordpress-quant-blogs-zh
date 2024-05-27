<!--yml

类别：未分类

日期：2024-05-18 15:13:49

-->

# 及时投资组合：按评级划分的债券风险与回报

> 来源：[`timelyportfolio.blogspot.com/2011/06/bonds-risk-and-return-by-rating.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/06/bonds-risk-and-return-by-rating.html#0001-01-01)

```
#do everything twice to compare monthly average to daily    require(RQuantLib)
require(quantmod)
require(PerformanceAnalytics) 
require(ggplot2)   getSymbols("AAA",src="FRED") # load Moody's AAA from Fed Fred 
getSymbols("BAA",src="FRED") # load Moody's BAA from Fed Fred    #Fed monthly series of yields is the monthly average of daily yields
#set index to yyyy-mm-dd format rather than to.monthly mmm yyy for better merging later
index(AAA)<-as.Date(index(AAA))
index(BAA)<-as.Date(index(BAA))
AAApricereturn<-AAA
BAApricereturn<-BAA   AAApricereturn[1,1]<-0
BAApricereturn[1,1]<-0
colnames(AAApricereturn)<-"PriceReturn-monthly avg AAA"
colnames(BAApricereturn)<-"PriceReturn-monthly avg BAA"
#use quantlib to price the AAA and BAA bonds from monthly yields
#AAA and BAA series are 20-30 year bonds so will advance date by 25 years
for (i in 1:(NROW(AAA)-1)) {
  AAApricereturn[i+1,1]<-FixedRateBondPriceByYield(yield=AAA[i+1,1]/100,issueDate=Sys.Date(), 
    maturityDate= advance("UnitedStates/GovernmentBond", Sys.Date(), 25, 3),
    rates=AAA[i,1]/100,period=2)[1]/100-1
} 
for (i in 1:(NROW(BAA)-1)) {
  BAApricereturn[i+1,1]<-FixedRateBondPriceByYield(yield=BAA[i+1,1]/100,issueDate=Sys.Date(), 
    maturityDate= advance("UnitedStates/GovernmentBond", Sys.Date(), 25, 3),
    rates=BAA[i,1]/100,period=2)[1]/100-1
}   #total return will be the price return + yield/12 for one month
AAAtotalreturn<-AAApricereturn+lag(AAA,k=1)/12/100
colnames(AAAtotalreturn)<-"TotalReturn-monthly avg AAA" 
BAAtotalreturn<-BAApricereturn+lag(BAA,k=1)/12/100
colnames(BAAtotalreturn)<-"TotalReturn-monthly avg BAA"   charts.PerformanceSummary(merge(AAApricereturn,AAAtotalreturn,BAApricereturn,BAAtotalreturn),ylog=TRUE,
	colorset=c("cadetblue","darkolivegreen3","purple","goldenrod"),
	main="Simulated Returns from Moody's AAA and BAA Yield")
mtext("Source: Federal Reserve FRED",side=1,adj=0)   AAA_BAA <- na.omit(merge(AAAtotalreturn,BAAtotalreturn))
#get df for ggplot
df <- as.data.frame(cbind(index(AAA_BAA),coredata(AAA_BAA[,1:2])))
df[,1] <- paste(substr(format(as.Date(df[,1]),"%Y"),1,3),0,sep="")
colnames(df) <- c("Decade","AAA","BAA")
dfmelt <- melt(df,id.vars=1)
colnames(dfmelt) <- c("Decade","Moodys_Rating","TotalReturn")
dfsum <- ddply(dfmelt, .(Decade,Moodys_Rating), summarise,
	mean = mean(TotalReturn),
	sd = sd(TotalReturn))
jpeg(filename="risk and return by rating.jpg",quality=100,width=6.25, height = 5, 
 units="in",res=96)
ggplot(dfsum, aes(x=sd,y=mean,label=factor(Decade))) + geom_point(aes(colour=Moodys_Rating)) +
	geom_line(aes(x=sd,y=mean,colour=Moodys_Rating)) + geom_text(aes(colour=Moodys_Rating)) +
	opts(title="Risk (sd) and Return (mean) by Moodys Rating since 1919")
dev.off()     ####some other experimentation but not part of blog post
getSymbols("DJTA",src="FRED")
getSymbols("DJIA",src="FRED")
#convert to monthly and get monthly returns
DJTA <- ROC(to.monthly(DJTA)[,4],n=1,type="discrete")
DJIA <- ROC(to.monthly(DJIA)[,4],n=1,type="discrete")
#set index to yyyy-mm-dd format rather than to.monthly mmm yyy for better merging later
index(DJTA)<-as.Date(index(DJTA))
index(DJIA)<-as.Date(index(DJIA))   #merge AAA,BAA,DJTA,DJIA
assetReturns <- na.omit(merge(AAAtotalreturn,BAAtotalreturn,DJTA,DJIA))   charts.PerformanceSummary(assetReturns,ylog=TRUE,
	colorset=c("cadetblue","darkolivegreen3","purple","goldenrod"),
	main="DJIA, DJTA, and Simulated Returns from Moody's AAA and BAA Yield")
mtext("Source: Federal Reserve FRED",side=1,adj=0)   chart.RiskReturnScatter(assetReturns["1950::1959",])
```
