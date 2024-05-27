<!--yml

category: 未分类

date: 2024-05-18 15:15:57

-->

# Timely Portfolio：Wonderful New Blog TimeSeriesIreland

> 来源：[`timelyportfolio.blogspot.com/2011/05/wonderful-new-blog-timeseriesireland.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/05/wonderful-new-blog-timeseriesireland.html#0001-01-01)

我从苏格兰回来发现了一个来自爱尔兰的精彩新博客[`timeseriesireland.wordpress.com`](http://timeseriesireland.wordpress.com)。为了突出他的工作，我想我会将他最近的一篇文章[AIB 股价、EGARCH-M 和 rgarch](http://timeseriesireland.wordpress.com/2011/05/17/aib-stock-price-egarch-m-and-rgarch/)应用于标普 500。显然，TimeSeriesIreland 的作者对时间序列统计有着比我更好的把握，所以我不会尝试更改滞后顺序或完善模型。相反，我将使用他的 AIB 日数据的模型规范来处理标普 500 的周数据。这应该会很有趣；也许这会引发一些评论。

另外，遗憾的是我需要声明，但**这仅供说明目的，不应视为投资建议。您对自己的收益和损失负责。**我基于 fittedmodel$z 构建了一个非常基本的系统，只是为了好玩。以下是结果。

R 代码：

#此代码的所有信用归功于非常有洞察力的作者

#来自[`timeseriesireland.wordpress.com`](http://timeseriesireland.wordpress.com)

#根据最初的几篇文章，我期待着关注他

#对于统计数据及其使用的解释，请参见

#[`timeseriesireland.wordpress.com/2011/05/17/aib-stock-price-egarch-m-and-rgarch/#more-295`](http://timeseriesireland.wordpress.com/2011/05/17/aib-stock-price-egarch-m-and-rgarch/#more-295)

#我更改了代码，使用 SP500 的周 xts 数据，而不是 AIB 的每日 tseries 数据

require(rgarch)

require(urca)

require(ggplot2)

require(quantmod)

require(PerformanceAnalytics)

#定义开始和结束日期

start<-"1929-01-01"

end<- format(Sys.Date(),"%Y-%m-%d") # yyyy-mm-dd

tckr<-"^GSPC"

#使用 quantmod 获取 SP500 数据

getSymbols(tckr,from=start,to=end)

GSPC<-to.weekly(GSPC)

#获取对数收益，也可以使用 type="continuous"的 ROC

LGSPC<-log(GSPC[,4])

retGSPC<-diff(LGSPC)

#数据框允许我们使用来自 xts 的日期数据进行 ggplot

#我还没有找到更好的方式来 ggplot xts 数据

df1<-data.frame(index(GSPC),coredata(GSPC[,4]))

colnames(df1)<-c("dates","sp500")

### 绘制标普 500 价格：

gg1.1<-ggplot(df1,aes(dates,sp500)) + xlab(NULL) + ylab("SP500 log Price") + scale_y_log10()

gg1.2<-gg1.1+geom_line(colour="darkblue") + opts(title="Weekly SP500 Price 1950-current")

gg1.2

#将第一个回报设置为 0

retGSPC[1]<-0

df2<-data.frame(index(retGSPC),coredata(retGSPC))

colnames(df2)<-c("dates","sp500")

gg2.1<-ggplot(df2,aes(dates,sp500)) + xlab(NULL) + ylab("Log Changes")

gg2.2<-gg2.1+geom_line(colour="darkred") + opts(title="Weekly SP500 Price Return")

gg2.2

### ACFs 和 PACFs

par(mfrow=c(2,1))

acf(retGSPC, main="ACF of SP500 Log Returns", lag = 50)

pacf(retGSPC, main="PACF of SP500 Log Returns", lag = 50)

ar9<-arima(retGSPC, order=c(9,0,0))

acf(ar9$residuals)

ressq<-(ar9$residuals)²

Box.test(ressq, lag = 8, type = "Ljung-Box")

pacf(ressq, main="PACF of Squared Residuals", lag = 30)

# Note that the GARCH order is revered from what I have discussed above

specm1 <- ugarchspec(variance.model=list(model="eGARCH", garchOrder=c(2,4), submodel = NULL),

mean.model=list(armaOrder=c(9,0), include.mean=TRUE, garchInMean = TRUE))

#this might take a while

fitm1 <- ugarchfit(data = retGSPC, spec = specm1)

fitm1

#plot(fitm1) #use option 8

fittedmodel <- fitm1@fit

sigma1<-fittedmodel$sigma

df2<-data.frame(index(retGSPC),coredata(retGSPC),sigma1)

colnames(df2)<-c("dates","sp500","sigma1")

gg3.1<-ggplot(df2,aes(dates)) + xlab(NULL) + ylab("Log Changes")

gg3.2<-gg3.1+geom_line(aes(y = sp500, colour="Log Returns")) + opts(title="Weekly Log Return with 2 Conditional Standard Deviations")

gg3.3<-gg3.2 + geom_line(aes(y = sigma1*2, colour="2 S.D.")) + geom_line(aes(y = sigma1*-2, colour="2 S.D.")) + scale_colour_hue("Series:") + opts(legend.position=c(.18,0.8))

gg3.3

fitm2 <- ugarchfit(data = retGSPC,out.sample = 10, spec = specm1)

fitm2

pred <- ugarchforecast(fitm2, n.ahead = 10,n.roll = 0)

pred.fpm <- fpm(pred)

pred.fpm

#just because I cannot stand it

#I'll play with a system

#not something I would bet my money on

signal<-runMean(as.xts(fittedmodel$z,order.by=index(retGSPC)),50)

#chartSeries(signal)

signal<-lag(signal,k=1)

signal[is.na(signal)]<-0

ret<-ifelse(signal > 0,ROC(GSPC[,4],1,type="discrete"),0)

returnCompare<-merge(ret,ROC(GSPC[,4],1,type="discrete"))

colnames(returnCompare)<-c("ZSystem","SP500")

charts.PerformanceSummary(returnCompare,ylog=TRUE,main="Just for Fun Z System")
