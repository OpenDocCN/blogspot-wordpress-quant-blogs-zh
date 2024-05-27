<!--yml

类别：未分类

日期：2024-05-18 15:15:45

-->

# 及时投资组合：长期 XLU 短期 SPY 第二部分（更多历史）

> 来源：[`timelyportfolio.blogspot.com/2011/05/long-xlu-short-spy-part-2-more-history.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/05/long-xlu-short-spy-part-2-more-history.html#0001-01-01)

**这不是投资建议。 您对自己的收益和损失负责。**

美联储正在不断增加 BAC ML 债券指数，现在是四个主要道琼斯指数的完整历史，所以我想扩展我的第一篇文章[长期 XLU 短期 SPY](http://timelyportfolio.blogspot.com/2011/05/long-xlu-short-spy.html)以增加一些更多的历史背景。 不幸的是，道琼斯指数只是价格回报，但我认为探索仍然有益于讨论。 包括股利显着增强了价差头寸。

现在有美国 10 年期国库券价格回报系列。详情请参见[历史债券回报来源-日度与月度比较](http://timelyportfolio.blogspot.com/2011/04/historical-sources-of-bond-returns_17.html)有关美国 10 年期国库券回报计算的详细信息。

最初的讨论是作为一个债券经理，如果我不喜欢债券我可以做什么。 让我们快速看一下长期 DJUA 短期 US10y 价格差价，看看在这种情况下它将如何运作。 以上的相关性确实很吸引人。

R 代码:

#获得更多历史

require(RQuantLib)

require(PerformanceAnalytics)

require(quantmod)

#首先债券

getSymbols("DGS10",src="FRED") #加载每日美国财政部 10 年期国库券

DGS10pricereturn<-DGS10  #设置这个来保存价格回报

DGS10pricereturn[1,1]<-0

colnames(DGS10pricereturn)<-"PriceReturn-daily to monthly DGS10"

#我知道我需要向量化这个但还不够资格

#请随意评论以告诉我如何做到这一点

for (i in 1:(NROW(DGS10)-1)) {

DGS10pricereturn[i+1,1]<-FixedRateBondPriceByYield(yield=DGS10[i+1,1]/100,issueDate=Sys.Date(),

到期日= advance("UnitedStates/GovernmentBond", Sys.Date(), 10, 3),

rates=DGS10[i,1]/100,period=2)[1]/100-1

}

#总回报将是价格回报+一个月的收益/12

DGS10totalreturn<-DGS10pricereturn+lag(DGS10,k=1)/12/100

colnames(DGS10totalreturn)<-"Total Return-daily to monthly DGS10"

#现在是道琼斯指数

getSymbols("DJIA",src="FRED") #加载每日道琼斯工业

getSymbols("DJUA",src="FRED") #加载每日道琼斯公用事业

DJUADJIA<-DJUA/DJIA

retDJ<-na.omit(merge(ROC(DJUADJIA,1,type="discrete"),ROC(DJIA,1,type="discrete"),ROC(DJUA,1,type="discrete")))

colnames(retDJ)<-c("DJIA","DJUA","DJUADJIAspread")

charts.PerformanceSummary(retDJ,ylog=TRUE,

主要="DJIA，DJUA 和 DJUA/DJIA 差价价格回报分析",

colorset=c("cadetblue","darkolivegreen3","goldenrod"))

#现在将债券添加到分析中

retToAnalyze<-na.omit(merge(ROC(DJIA,1,type="discrete"),

ROC(DJUA,1,type="discrete"),

ROC(DJUA/DJIA,1,type="discrete"),

DGS10pricereturn))

colnames(retToAnalyze)<-c("DJIA","DJUA","DJUADJIAspread","US10yPrice")

`charts.PerformanceSummary(retToAnalyze,ylog=TRUE,

`main="DJIA, DJUA, DJUA/DJIA Spread, and US 10y Price Return Analysis",

colorset=c("cadetblue","darkolivegreen3","goldenrod","gray70"))`

`chart.Correlation(retToAnalyze)`

`corDJUADJIAtoDJIA<-runCor(retDJ[,1],retDJ[,2],120)`

`corDJUADJIAtoBonds<-runCor(retToAnalyze[,3],retToAnalyze[,4],120)`

`chartSeries(DJUADJIA,TA="addTA(corDJUADJIAtoDJIA);addTA(corDJUADJIAtoBonds)",

`theme="white",

name="Long DJUA and Short DJIA with Correlation Analysis")`

`#now let's see how it looks as long xlu short bonds on price basis`

priceBonds<-na.omit(cbind(DGS10pricereturn,rep(1,NROW(DGS10))))`

priceBonds<-cumprod(priceBonds[,1]+priceBonds[,2])`

DJUABonds<-na.omit(merge(DJUA,priceBonds))`

`DJUABonds<-DJUABonds[,1]/DJUABonds[,2]`

`chartSeries(DJUABonds, log=TRUE,

theme="white",

`name="Long DJUA and Short Bonds Price")`
