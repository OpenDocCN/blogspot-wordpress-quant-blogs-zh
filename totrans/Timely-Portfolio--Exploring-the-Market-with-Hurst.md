<!--yml
category: 未分类
date: 2024-05-18 15:14:14
-->

# Timely Portfolio: Exploring the Market with Hurst

> 来源：[http://timelyportfolio.blogspot.com/2011/06/exploring-market-with-hurst.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/06/exploring-market-with-hurst.html#0001-01-01)

Randomly trudging through PerformanceAnalytics source code, I was intrigued by the [Hurst Index calculation](https://r-forge.r-project.org/scm/viewvc.php/pkg/PerformanceAnalytics/R/HurstIndex.R?view=markup&root=returnanalytics), which I discovered is more commonly called [Hurst Exponent](http://en.wikipedia.org/wiki/Hurst_exponent).  After quickly satisfying myself that I could actually do the rolling Hurst calculation in R, I wanted to see how this small discovery might be applied to market research and trading systems.  I found a couple of interesting articles through a [Google Scholar search](http://scholar.google.com/scholar?hl=en&q=hurst+exponent&as_sdt=1%2C1&as_ylo=&as_vis=0), and away I went.

The first interesting paper Bo Qian and Khaled Rasheed ["HURST EXPONENT AND FINANCIAL MARKET PREDICTABILITY](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.137.207&rep=rep1&type=pdf) demonstrated something I have noticed but not proven over the last 10 years of system building.  Based on the chart below, the Hurst exponent for 1950-1980 seems very different than 1980 (especially 1990)-2004.  This would fit my unscientific observation that momentum/trend-following strategies worked best 1950-1980 (Hurst > 0.55) and mean reversion performed best for 1980-2004 (Hurst < 0.5).

I had some trouble replicating and extending the Hurst exponent calculation from the paper to the entire set 1896-2011.  The Hurst exponent should oscillate mainly between 0.4 and 0.6 with an average 0.54 on a random unstructured series based on the paper’s simulations and my understanding.  As seen below my results are dramatically different and clearly wrong with a Hurst exponent oscillating between 0.35 and 0.5.  If I change the calculation period and apply a rolling average, I get more reasonable but still incorrect results.  This happens whether I apply to daily, weekly, or monthly returns.  It seems that the calculation fails at periods > 12 months.

What I found is that the Hurst exponent calculation is an estimation and could vary widely based on the technique.  The calculation in PerformanceAnalytics is clearly not the same as that presented in the paper.  I evidently fell into the same Hurst trap that has confronted many market students and described at this site [http://www.bearcave.com/misl/misl_tech/wavelets/hurst/index.html](http://www.bearcave.com/misl/misl_tech/wavelets/hurst/index.html "http://www.bearcave.com/misl/misl_tech/wavelets/hurst/index.html") found by a Google search:

> “Sadly things frequently are not as simple as they seem. Looking back, there are a number of things that I did not understand:
> 
> 1.  The Hurst exponent is not so much calculated as estimated. A variety of techniques exist for doing this and the accuracy of the estimation can be a complicated issue.
>     
>     
> 2.  Testing software to estimate the Hurst exponent can be difficult. The best way to test algorithms to estimate the Hurst exponent is to use a data set that has a known Hurst exponent value. Such a data set is frequently referred to as *fractional brownian motion* (or fractal gaussian noise). As I learned, generating fractional brownian motion data sets is a complex issue. At least as complex as estimating the Hurst exponent.
>     
>     
> 3.  The evidence that financial time series are examples of long memory processes is mixed. When the hurst exponent is estimated, does the result reflect a long memory process or a short memory process, like autocorrelation? Since autocorrelation is related to the Hurst exponent (see Equation 3, below), is this really an issue or not?
>     
>     
> 
> I found that I was not alone in thinking that the Hurst exponent might provide interesting results when applied to financial data. The intuitively fractal nature of financial data (for example, the 5-day return time series in Figure 5) has lead a number of people to apply the mathematics of fractals and chaos analyzing these time series.”

The beautiful thing about R though is the high likelihood of another package that will calculate Hurst.  I chose FGN in search of a better result.  The results makes more sense but still does not match the observations in the paper.  However the stronger momentum 1950-1980 and stronger mean reversion 1980-2010 still appear.  This might help explain [http://www.automated-trading-system.com/turtles-just-lucky/](http://www.automated-trading-system.com/turtles-just-lucky/ "http://www.automated-trading-system.com/turtles-just-lucky/").

I am sure that many brilliant mathematicians have applied the Hurst exponent profitably, but as of now, too much vagueness and uncertainty exist for me to bet my or my client’s money on it.  However, as always, I thought I would try to build a system with the Hurst exponent.  In the paper, the authors imply that for best results focus on times with a high Hurst exponent.

**IT IS ASHAME THAT I MUST DISCLAIM.  DO NOT TRADE THIS SYSTEM.  IT COULD LOSE LOTS OF MONEY.**

[R code (click to download):](https://docs.google.com/leaf?id=0B2qp2r96khJPNDE2NDhlNGQtNWY5NS00YTQ4LWFjODEtNDc2YWU3NmYxYWY1&hl=en_US)

```
require(quantmod)
require(PerformanceAnalytics)   #get DJIA since 1896 from St. Louis Fed Fred
getSymbols("DJIA",src="FRED")   #do monthly to shorten the lengthy calculation
#on my old computer
DJIA <- to.monthly(DJIA)[,4]
retDJIA <- ROC(DJIA,n=1,type="discrete")   #paper HURST EXPONENT AND FINANCIAL MARKET PREDICTABILITY by
#Bo Qian and Khaled Rasheed use 1024 days or 4 years
#or 208 weeks assuming 52 weeks/year
#I first tried HurstIndex from PerformanceAnalytics
hurst.48 <- apply.rolling(retDJIA, FUN="HurstIndex", width=48)
chart.TimeSeries(hurst.208,colorset=c("cadetblue"),
	main = "Hurst Index (48 Month) for DJIA
	1896-2011")
#my results are very different from the research paper whether I use
#daily, weekly, or monthly
#so I must be doing something wrong
hurst.avg <- apply.rolling(retDJIA, FUN="HurstIndex", width=12)
hurst.avg <- runMean(hurst.avg,n=48)
hurst <- merge(hurst.48,hurst.avg)
colnames(hurst) <- c("Hurst 48 Month","Hurst 4y Avg of 12 Month")
chart.TimeSeries(hurst,colorset=c("cadetblue","darkolivegreen3"),
	legend.loc="bottomright",
	main = "Hurst Index Comparison for DJIA
	1896-2011")
abline(h=0.5) #this represents no trend or mean reversion     #now let's try a different package
require(FGN)
#get DJIA since 1896 from St. Louis Fed Fred
getSymbols("DJIA",src="FRED")
#will do daily; takes about 2 hours
#on my old computer
DJIA <- DJIA
retDJIA <- ROC(DJIA,n=1)
#about 2 hours for a result on my old computer
hurstK <- apply.rolling(retDJIA, FUN="HurstK", width=1024)
chart.TimeSeries(hurstK,colorset=c"cadetblue",
	main = "HurstK Calculation of Hurst Exponent (1024 days) for DJIA
	1896-2011")     #######system-building time
#do monthly just to test more quickly
DJIA <- to.monthly(DJIA)[,4]
index(DJIA) <- as.Date(index(DJIA))
retDJIA<-ROC(DJIA,n=1,type="discrete")
index(retDJIA) <- as.Date(index(retDJIA))
hurstKmonthly <- apply.rolling(retDJIA, FUN="HurstK", width = 12)
colnames(hurstKmonthly) <- "HurstK.monthly"
index(hurstKmonthly) <- as.Date(index(hurstKmonthly))
serialcorr <- runCor(cbind(coredata(retDJIA)),cbind(index(retDJIA)),n=12)
serialcorr <- as.xts(serialcorr,order.by=index(retDJIA))
autoreg <- runCor(retDJIA,lag(retDJIA,k=1),n=12)
colnames(serialcorr) <- "SerialCorrelation.monthly"
colnames(autoreg) <- "AutoRegression.monthly"
#check for correlation of potential signals
chart.Correlation(merge(hurstKmonthly,serialcorr,autoreg))
#try a sum to enter in strong trends
signal <- hurstKmonthly+serialcorr+autoreg
colnames(signal) <- "HurstCorrelationSum"
chart.TimeSeries(signal)
signal <- lag(signal,k=1)
retSys <- ifelse(signal > 0.1, 1, 0) * retDJIA
#charts.PerformanceSummary(retSys,ylog=TRUE)
#ok performance but let's see if we can enter
#only strong trends up and reduce the drawdown
signalUpTrend <- runMean(hurstKmonthly+serialcorr+autoreg,n=6) + (DJIA/runMean(DJIA,n=12)-1)*10
chart.TimeSeries(signalUpTrend)
signalUpTrend <- lag(signalUpTrend,k=1)
retSys <- merge(retSys,ifelse(signalUpTrend > 1, 1, 0) * retDJIA,retDJIA)
colnames(retSys) <- c("DJIA Hurst System","DJIA HurstUp System",
	"DJIA")
charts.PerformanceSummary(retSys,ylog=TRUE,cex.legend=1.25,
	colorset=c("cadetblue","darkolivegreen3","gray70"))   #now let's take it out of sample to see how it works
getSymbols("^N225",from="1980-01-01",to=format(Sys.Date(),"%Y-%m-%d"))
N225 <- to.monthly(N225)[,4]
index(N225) <- as.Date(index(N225))
retN225<-ROC(N225,n=1,type="discrete")
index(retN225) <- as.Date(index(retN225))
hurstKmonthly <- apply.rolling(retN225, FUN="HurstK", width = 12)
colnames(hurstKmonthly) <- "HurstK.monthly"
index(hurstKmonthly) <- as.Date(index(hurstKmonthly))
serialcorr <- runCor(cbind(coredata(retN225)),cbind(index(retN225)),n=12)
serialcorr <- as.xts(serialcorr,order.by=index(retN225))
autoreg <- runCor(retN225,lag(retN225,k=1),n=12)
colnames(serialcorr) <- "SerialCorrelation.monthly"
colnames(autoreg) <- "AutoRegression.monthly"
signalUpTrend <- runMean(hurstKmonthly+serialcorr+autoreg,n=6) + (N225/runMean(N225,n=12)-1)*10
chart.TimeSeries(signalUpTrend)
signalUpTrend <- lag(signalUpTrend,k=1)
retSys <- merge(ifelse(signalUpTrend > 1, 1, 0) * retN225,retN225)
colnames(retSys) <- c("Nikkei 225 HurstUp System","Nikkei 225")
charts.PerformanceSummary(retSys,ylog=TRUE,cex.legend=1.25,
	colorset=c("cadetblue","darkolivegreen3"))
###########################
```

[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")