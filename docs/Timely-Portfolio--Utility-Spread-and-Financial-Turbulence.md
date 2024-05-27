<!--yml

类别：未分类

date：2024-05-18 15:15:41

-->

# 及时投资组合：效用价差和金融动荡

> 来源：[`timelyportfolio.blogspot.com/2011/05/utility-spread-and-financial-turbulence.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/05/utility-spread-and-financial-turbulence.html#0001-01-01)

**这不是投资建议。您对自己的收益和损失负责。**

在[Long XLU Short SPY Part 2 (More History)](http://timelyportfolio.blogspot.com/2011/05/long-xlu-short-spy-part-2-more-history.html)中，我探讨了这种价差的防御性质及其在股票困难时期作为债券替代品的潜力。我想看到如果我们在[Great FAJ Article on Statistical Measure of Financial Turbulence Part 3](http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical_6197.html)系统中将这种价差作为我们的现金持仓，会发生什么。不幸的是，将价格回报中的价差用作现金并不像将债券用作现金那样有利于系统，但我仍然认为这可能会鼓励一些对价差及其潜在用途的额外思考。

R 代码：

require(quantmod)

require(PerformanceAnalytics)

#从圣路易斯联邦储备局（FRED）获取数据

getSymbols("GS20",src="FRED") #加载 20 年期国债；20 年期在 1986 年至 1993 年之间有间隙；30 年期在 2000 年代初有间隙

getSymbols("GS30",src="FRED") #加载 30 年期国债，以填补 20 年期国债在 1986 年至 1993 年之间的间隙

getSymbols("BAA",src="FRED") #加载 BAA

getSymbols("SP500",src="FRED") #加载 SP500

#现在是道琼斯指数

getSymbols("DJIA",src="FRED") #加载每日道琼斯工业平均指数

getSymbols("DJUA",src="FRED") #加载每日道琼斯公用事业平均指数

DJUADJIA<-DJUA/DJIA

#从 csv 文件获取 CRB 数据

CRB<-as.xts(read.csv("crb.csv",row.names=1))[,1]

#使用已停止发行的 20 年期国债填补 1986 年至 1993 年之间的 20 年期间隙

GS20["1987-01::1993-09"]<-GS30["1987-01::1993-09"]

#稍微操作一下，以便数据在每月基础上对齐

SP500<-to.monthly(SP500)[,4]

DJUADJIA<-to.monthly(DJUADJIA)[,4]

#将格式更改为每月的 yyyy-mm-dd，第一天为该月的第一天

index(SP500)<-as.Date(index(SP500))

index(DJUADJIA)<-as.Date(index(DJUADJIA))

#我的 CRB 数据是月末的；可以更改，但在 R 中更有趣

CRB<-to.monthly(CRB)[,4]

index(CRB)<-as.Date(index(CRB))

#让我们将所有这些合并成一个 xts 对象；CRB 从 1956 年开始

assets<-na.omit(merge(GS20,SP500,CRB,DJUADJIA))

#使用 SP500 和 CRB 的 ROC，以及收益数据的动量

assetROC<-na.omit(merge(momentum(assets[,1])/100,ROC(assets[,2:4],type="discrete")))

#获取相关性

corrBondsSp<-runCor(assetROC[,1],assetROC[,2],n=7)

corrBondsCrb<-runCor(assetROC[,1],assetROC[,3],n=7)

corrSpCrb<-runCor(assetROC[,2],assetROC[,3],n=7)

#资产类别之间的相关性的复合度量和 ROC 加权相关性

assetCorr<-(corrBondsSp+corrBondsCrb+corrSpCrb+

(corrBondsSp*corrSpCrb*assetROC[,2])+

(corrBondsCrb*corrSpCrb*assetROC[,3])-

assetROC[,1])/6

#资产类别的 ROC 总和

assetROCSum<-assetROC[,1]+assetROC[,2]+assetROC[,3]

#最后是动荡测量

turbulence<-abs(assetCorr*assetROCSum*100)

colnames(turbulence)<-"动荡-相关性"

chartSeries(turbulence,theme="white",name="相关性和%变化作为金融动荡的衡量")

abline(h=0.8)

chart.ACF(turbulence,main="动荡的自相关性")

#但愿我能记得我从哪里得到了一些代码

#最有可能的候选人是 www.fosstrading.com

#如果您知道来源，请告诉我

#这样我就能给予充分的认可

#使用动荡来确定是否持有等权重的标准普尔 500 指数和商品 Research Bureau 指数

signal<-ifelse(turbulence>0.8,0,1)

#使用标准普尔 500 指数/商品 Research Bureau 指数的斜率来确定标准普尔 500 指数或商品 Research Bureau 指数

signal<-lag(signal,k=1)

# 用“no position”替换缺失的信号

# (一般只在系列的开始时)

signal[is.na(signal)] <- 0

#从等权重的商品 Research Bureau 指数和标准普尔 500 指数持仓中获取回报；Return.portfolio 导致问题，所以采用了更麻烦的方法

ret<-ifelse(signal==1,(assetROC[,2]+assetROC[,3])/2,assetROC[,4])

ret[1] <- 0

#获取系统表现

system_perf <- ret*signal

system_perf_util <- ret

system_eq <- cumprod(1+signal*ret)

system_eq_util <- cumprod(1+ret)

perf_comparison<-merge(lag((assetROC[,2]+assetROC[,3])/2,k=1),system_perf,system_perf_util)

colnames(perf_comparison)<-c("等权重","带有动荡过滤器的系统","带有动荡过滤器的系统-带有实用性")

charts.PerformanceSummary(perf_comparison,ylog=TRUE,main="基于动荡的系统 vs 等权重 CRB 和 SP500")

#让我们使用基本的相对强度来选择标准普尔 500 指数或商品 Research Bureau 指数

#我知道我可以在 R 中做得更好，但这是我的丑陋代码

#计算标准普尔 500 指数/商品 Research Bureau 指数的 12 个月斜率

width=12

for (i in 1:(NROW(assets)-width)) {

model<-lm(assets[i:(i+width),2]/assets[i:(i+width),3]~index(assets[i:(i+width)]))

ifelse(i==1,assetSlope<-model$coefficients[2],assetSlope<-rbind(assetSlope,model$coefficients[2]))

}

assetSlope<-xts(cbind(assetSlope),order.by=index(assets)[(width+1):NROW(assets)])

#使用动荡来确定是否持有等权重的标准普尔 500 指数和商品 Research Bureau 指数

signal<-ifelse(turbulence>0.8,0,1)

#使用标准普尔 500 指数/商品 Research Bureau 指数的斜率来确定标准普尔 500 指数或商品 Research Bureau 指数

signal2<-ifelse(assetSlope[,1]>0,1,2)

signal<-lag(signal,k=1)

signal[1]<-0

signal2<-lag(signal2,k=1)

signal2[1]<-0

signals_and_returns<-merge(signal,signal2,assetROC,assetSlope,turbulence)

#当动荡较低时，根据斜率获取标准普尔 500 指数或商品 Research Bureau 指数的回报，或者使用债券作为现金

ret<-ifelse(signals_and_returns[,2]==1,signals_and_returns[,4],ifelse(signals_and_returns[,2]==2,signals_and_returns[,5],signals_and_returns[,3]))

#当动荡较低时，根据斜率获取标准普尔 500 指数或商品 Research Bureau 指数的回报，或者将实用性价差作为现金

ret_util<-ifelse(signals_and_returns[,2]==1&signals_and_returns[,1]==1,signals_and_returns[,4],

ifelse(signals_and_returns[,2]==2&signals_and_returns[,1]==1,signals_and_returns[,5],

signals_and_returns[,6]))

ret[1]<-0

ret_util[1]<-0

#获取系统表现

system_perf_rs<-signals_and_returns[,1]*ret

system_perf_rs_util<-ret_util

system_eq_rs<- cumprod(1+signals_and_returns[,1]*ret)

system_eq_rs_util<- cumprod(1+ret_util)

性能比较<-合并((资产 ROC[,2]+资产 ROC[,3])/2,资产 ROC[,2],资产 ROC[,3],系统性能,系统性能利用率,系统性能 RS,系统性能 RS 利用率)

性能比较的列名<-c("等权重","S&P500","CRB","带湍流过滤器的系统","带湍流过滤器的系统利用率","带湍流过滤器的系统与 RS 的组合","带湍流过滤器的系统与 RS 组合利用率")

图表.性能总结(性能比较, ylog=TRUE, 主标题="基于湍流的系统与 RS 的比较、等权重、CRB 和 SP500")
