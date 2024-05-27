<!--yml

类别: 未分类

日期: 2024-05-18 15:16:50

-->

# 及时投资组合: 标普 500 高贝塔和低波动指数以及 Powershares ETFs

> 来源：[`timelyportfolio.blogspot.com/2011/05/s-500-high-beta-and-low-volatility.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/05/s-500-high-beta-and-low-volatility.html#0001-01-01)

新的标普 500 高贝塔和低波动指数必定提供了有用的见解、概念或系统。现在，随着 Powershares 宣布推出这些指数的 ETFs [`www.invescopowershares.com/volatility/`](http://www.invescopowershares.com/volatility/ "http://www.invescopowershares.com/volatility/")，这些潜在的见解、概念或系统似乎都是可行的。这些指数可以在标普网站上以电子表格的形式获得

> [`www.standardandpoors.com/indices/sp-500-low-volatility/en/us/?indexId=spusa-500-usdw-lop-us-l--`](http://www.standardandpoors.com/indices/sp-500-low-volatility/en/us/?indexId=spusa-500-usdw-lop-us-l-- "http://www.standardandpoors.com/indices/sp-500-low-volatility/en/us/?indexId=spusa-500-usdw-lop-us-l--<br />") [`www.standardandpoors.com/indices/sp-500-high-beta/en/us/?indexId=spusa-500-usdw-hbp-us-l--`](http://www.standardandpoors.com/indices/sp-500-high-beta/en/us/?indexId=spusa-500-usdw-hbp-us-l--)

或者通过 SP5HBIT 和 SP5LVIT 来使用彭博社的 High Beta 和 Low Volatility.

如果我们应用之前文章介绍的一些基本的相对强度和动量技术，我们可以构建一个在高贝塔和低波动指数之间切换的策略。

或者使用相同的信号，我们可以使用相对强度（RS）信号来为整个标普 500 指数生成入场和出场信号。

R 代码:

require(quantmod)

require(PerformanceAnalytics)

#不认为可以直接从标普下载

#但可以从获取一个电子表格来使用

#[`www.standardandpoors.com/indices/sp-500-low-volatility/en/us/?indexId=spusa-500-usdw-lop-us-l--`](http://www.standardandpoors.com/indices/sp-500-low-volatility/en/us/?indexId=spusa-500-usdw-lop-us-l--)

#[`www.standardandpoors.com/indices/sp-500-high-beta/en/us/?indexId=spusa-500-usdw-hbp-us-l--`](http://www.standardandpoors.com/indices/sp-500-high-beta/en/us/?indexId=spusa-500-usdw-hbp-us-l--)

#这些指数也可以通过彭博社和路透社获得

#通过 RBloomberg 可以使用 Bloomberg 访问

SPHighBetaLowVol<-as.xts(read.csv("sphighbeta-lowvol.csv",row.names=1,stringsAsFactors=FALSE))

SPIndexes<-merge(SPHighBetaLowVol,getSymbols("^GSPC",from="2006-01-03",auto.assign=FALSE)[,4])

SPIndexesReturns<-ROC(SPIndexes,1,type="discrete")

charts.PerformanceSummary(SPIndexesReturns)

#让我们尝试一种简单的相对强度信号和指数过滤器

#我知道我可以在 R 中更好地完成这个任务，但这是我的丑陋代码

#计算高贝塔/低波动的 125 天或 1/2 年斜率

width=125

#获取高贝塔/低波动的相对强度斜率

对于 (i in 1:(SPIndexes 的行数-width)) {

model<-lm(SPIndexes[i:(i+width),1]/SPIndexes[i:(i+width),2]~index(SPIndexes[i:(i+width)]))

ifelse(i==1,indexRS<-model$coefficients[2],indexRS<-rbind(indexRS,model$coefficients[2]))

}

indexRS<-xts(cbind(indexRS),order.by=index(SPIndexes)[(width+1):NROW(SPIndexes)])

#获取较短期 75 天的总 S&P 斜率

width=75

for (i in 1:(NROW(SPIndexes)-width)) {

model<-lm(SPIndexes[i:(i+width),3]~index(SPIndexes[i:(i+width)]))

ifelse(i==1,indexSlope<-model$coefficients[2],indexSlope<-rbind(indexSlope,model$coefficients[2]))

}

indexSlope<-xts(cbind(indexSlope),order.by=index(SPIndexes)[(width+1):NROW(SPIndexes)])

signals<-na.omit(merge(lag(indexRS),lag(indexSlope),SPIndexesReturns))

ret<-ifelse(signals[,1]>0&signals[,2]>0,signals[,3],ifelse(signals[,1]<0&signals[,2]>0,signals[,4],0))

perf_compare<-merge(ret,SPIndexesReturns)

#为图表命名列

colnames(perf_compare)<-c("RotationSystem",colnames(perf_compare)[2:4])

charts.PerformanceSummary(perf_compare,main="Rotation System with S&P Indexes)

#现在让我们使用 RS 信号来确定整体 S&P 指数的买卖点

#当高波动性表现优于时做多 S&P 500

ret<-ifelse(signals[,1]>0,signals[,5],0)

perf_compare<-merge(ret,perf_compare)

colnames(perf_compare)<-c("SP500TacticalBasedOnRS",colnames(perf_compare)[2:5])

charts.PerformanceSummary(perf_compare,main="Systems Comparisons with S&P Indexes)
