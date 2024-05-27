<!--yml

category: 未分类

date: 2024-05-18 15:14:14

-->

# Timely Portfolio: Exploring the Market with Hurst

> 来源：[`timelyportfolio.blogspot.com/2011/06/exploring-market-with-hurst.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/06/exploring-market-with-hurst.html#0001-01-01)

在 PerformanceAnalytics 源代码中随意浏览，我对其[Hurst 指数计算](https://r-forge.r-project.org/scm/viewvc.php/pkg/PerformanceAnalytics/R/HurstIndex.R?view=markup&root=returnanalytics)产生了兴趣，我发现这通常被称为[Hurst 指数](http://en.wikipedia.org/wiki/Hurst_exponent)。在确认我实际上可以在 R 中执行滚动 Hurst 计算后，我想看看这个小小的发现如何应用于市场研究和交易系统。通过[谷歌学术搜索](http://scholar.google.com/scholar?hl=en&q=hurst+exponent&as_sdt=1%2C1&as_ylo=&as_vis=0)，我找到了几篇有趣的文章，然后就出发了。

The first interesting paper Bo Qian and Khaled Rasheed ["HURST EXPONENT AND FINANCIAL MARKET PREDICTABILITY](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.137.207&rep=rep1&type=pdf) demonstrated something I have noticed but not proven over the last 10 years of system building.  Based on the chart below, the Hurst exponent for 1950-1980 seems very different than 1980 (especially 1990)-2004.  This would fit my unscientific observation that momentum/trend-following strategies worked best 1950-1980 (Hurst > 0.55) and mean reversion performed best for 1980-2004 (Hurst < 0.5).

我在将 Hurst 指数计算从论文扩展到整个 1896-2011 数据集时遇到了一些麻烦。根据论文的模拟和我所理解，Hurst 指数应该主要在 0.4 和 0.6 之间振荡，平均值为 0.54，这是一个基于随机无结构序列的。但正如下面所示，我的结果与预期相差甚远，Hurst 指数在 0.35 到 0.5 之间振荡，明显是错误的。如果改变计算周期并应用移动平均，我得到了更合理但仍然错误的结果。不管我应用到日回报、周回报还是月回报，都会出现这种情况。对于周期大于 12 个月的计算，似乎都失败了。

我发现 Hurst 指数的计算是一种估计，并且根据技术手段的不同，计算结果可能会有很大差异。PerformanceAnalytics 中的计算明显与论文中提出的计算不同。我显然落入了 Hurst 陷阱，许多市场学者都曾面临过同样的困境，并在此网站[`www.bearcave.com/misl/misl_tech/wavelets/hurst/index.html`](http://www.bearcave.com/misl/misl_tech/wavelets/hurst/index.html "http://www.bearcave.com/misl/misl_tech/wavelets/hurst/index.html")（通过谷歌搜索找到的）中描述过：

> “遗憾的是，事情往往不像它们看起来那么简单。回顾过去，有许多事情我并不理解：
> 
> 1.  Hurst 指数并不是计算出来的，而是估计出来的。存在各种技术用于此目的，估计的准确性可能是一个复杂的问题。
> 1.  
> 1.  测试估计 Hurst 指数的软件可能很难。测试估计 Hurst 指数算法的最佳方法是使用一个已知 Hurst 指数值的数据集。这样的数据集常被称为**分数布朗运动**（或分形高斯噪声）。据我所知，生成分数布朗运动数据集是一个复杂的问题。至少和估计 Hurst 指数一样复杂。
> 1.  
> 1.  金融时间序列是长记忆过程例子的证据是混合的。当估计 Hurst 指数时，结果反映的是长记忆过程还是短期记忆过程，比如自相关？由于自相关与 Hurst 指数有关（参见下面的方程 3），这真的是一个问题吗？
> 1.  
> 我发现认为当 Hurst 指数应用于金融数据时可能会提供有趣结果的想法并不孤独。金融数据直观的分形特性（例如，图 5 中的 5 天回报时间序列）使许多人将这些时间序列的分析应用到分形和混沌的数学上。”

**R 语言的优美之处在于很可能会有另一个包能计算 Hurst 指数。我选择 FGN 是为了得到更好的结果。结果更有说服力，但仍与论文中的观察不符。然而，1950-1980 年间的动量更强，1980-2010 年间的均值回归更强，这一现象仍然存在。这可能有助于解释**[`www.automated-trading-system.com/turtles-just-lucky/`](http://www.automated-trading-system.com/turtles-just-lucky/)**。

我确信许多杰出的数学家已经将 Hurst 指数应用于盈利，但就目前而言，对于我或我的客户的钱来说，还存在太多的模糊性和不确定性。然而，像往常一样，我想尝试建立一个带有 Hurst 指数的系统。在论文中，作者暗示为了获得最佳效果，应关注 Hurst 指数较高的时期。

**我必须声明这是一个遗憾。不要交易这个系统。它可能会损失很多钱。**

[R 代码（点击下载）：](https://docs.google.com/leaf?id=0B2qp2r96khJPNDE2NDhlNGQtNWY5NS00YTQ4LWFjODEtNDc2YWU3NmYxYWY1&hl=en_US)

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

[由 Pretty R 在 inside-R.org 创建](http://www.inside-r.org/pretty-r "由 Pretty R 在 inside-R.org 创建")
