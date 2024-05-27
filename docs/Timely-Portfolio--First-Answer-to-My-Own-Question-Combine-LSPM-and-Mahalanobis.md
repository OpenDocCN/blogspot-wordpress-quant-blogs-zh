<!--yml

分类：未分类

日期：2024-05-18 15:17:46

-->

# 及时投资组合：对自己的问题首次回答-组合 LSPM 和马氏距离

> 来源：[`timelyportfolio.blogspot.com/2011/05/first-answer-to-my-own-question-combine.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/05/first-answer-to-my-own-question-combine.html#0001-01-01)

我首先想感谢

[`www.fosstrading.com`](http://www.fosstrading.com/)

对于周末期间非常友好和意外的提及。你会注意到我代码中几乎都包含一些对 Foss Trading 的信用，感谢他们提供的示例和优秀的包。我讨厌我不能加入

[R/Finance 2011: 应用 R 的金融会议](http://rinfinance.com/)

上周末。

在我上一篇文章

[LSPM 在战术资产配置中的另一种用途](http://timelyportfolio.blogspot.com/2011/04/another-use-of-lspm-in-tactical.html)

, 我表达了对最终系统经历回撤的一点点挫折。由于我没有收到关于改进的评论或反馈，我猜我得尝试自己回答我的问题，“我如何减少回撤？” 我第一个想法是使用我在前一组文章中展示的技术

[Great FAJ Article on Statistical Measure of Financial Turbulence Part 3](http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical_6197.html)

关于

[马氏距离](http://en.wikipedia.org/wiki/Mahalanobis_distance)

作为金融动荡的衡量标准。

![faj 摘要](http://www.cfapubs.org/doi/abs/10.2469/faj.v66.n5.3)

结果表明，最大回撤和其他下行指标有所改善，但最终并不能满足我不断追求的更小的回撤。

| 无论如何，也许你可以使用我关于 PerformanceAnalytics 表的 ggplot2 图表。我很兴奋能成功做到这一点，并计划在测试中加入更多这样的图表。![](https://picasaweb.google.com/lh/photo/5VQD5b1wogWh74y3xF1QLw?feat=embedwebsite) |
| --- |
| 来自[TimelyPortfolio](https://picasaweb.google.com/kentonlrussell/TimelyPortfolio02?feat=embedwebsite) |

我写博客是为了记录我的想法，并希望能与我读者产生有价值的对话，他们可能比我还聪明和有资格。请评论或提供反馈。

R 代码：

#请参见 au.tra.sy 博客

[`www.automated-trading-system.com/`](http://www.automated-trading-system.com/)

#对于原始前进/优化代码和

[`www.fosstrading.com`](http://www.fosstrading.com/)

#对于其他技巧

需要(PerformanceAnalytics)

需要(quantmod)

需要(RQuantLib)

需要(reshape2) #为了某些花哨的 ggplot 图表

需要(ggplot2)

#获取债券回报以避免专有数据问题

#参见之前的 timelyportfolio 博客文章解释

#可能需要将这变成一个函数，因为我将大量使用

getSymbols("GS10",src="FRED") #从 Fed Fred 加载美国国债 10y

GS10pricereturn<-GS10  #设置此项以保存价格回报

GS10pricereturn[1,1]<-0

colnames(GS10pricereturn)<-"价格回报"

#我知道我需要对此进行向量化，但还不够资格

#请随意评论以向我展示如何操作

for (i in 1:(NROW(GS10)-1)) {

GS10pricereturn[i+1,1]<-FixedRateBondPriceByYield(yield=GS10[i+1,1]/100,issueDate=Sys.Date(),

maturityDate= advance("UnitedStates/GovernmentBond", Sys.Date(), 10, 3),

rates=GS10[i,1]/100,period=2)[1]/100-1

}

#每个月的利息回报将是收益率/12

GS10interestreturn<-lag(GS10,k=1)/12/100

colnames(GS10interestreturn)<-"利息回报"

#总回报将是价格回报 + 利息回报

GS10totalreturn<-GS10pricereturn+GS10interestreturn

colnames(GS10totalreturn)<-"债券总回报"

#从 FRED 获取 sp500 回报

getSymbols("SP500",src="FRED") #加载 SP500

#不幸的是，无法为专有 CRB 数据获得替代品

#从 csv 文件获取数据系列

CRB<-as.xts(read.csv("spxcrbndrbond.csv",row.names=1))[,2]

#对数据进行一些操作以使其在月度基础上对齐

GS10totalreturn<-to.monthly(GS10totalreturn)[,4]

SP500<-to.monthly(SP500)[,4]

# 将月度格式更改为 yyyy-mm-dd，以月初为准

index(SP500)<-as.Date(index(SP500))

#我的 CRB 数据是月底;可以更改，但在 R 中更有趣

CRB<-to.monthly(CRB)[,4]

index(CRB)<-as.Date(index(CRB))

#现在让我们合并以获取资产类别回报

assetROC<-na.omit(merge(ROC(SP500,type="discrete"),CRB,GS10totalreturn))

# 设置前向步数（周期数）

optim<-12 #1 年=12 个月的回报

wf<-1 #每月进行一次前向回报

numsys<-2

# 计算 WF 周期数

numCycles = floor((nrow(assetROC)-optim)/wf)

# 定义 JPT 函数

# 现在这已经成为 LSPM 包的一部分，但在没有负回报时会失败

# 所以我仍然在能够强制负回报的地方包含这个

jointProbTable <- function(x, n=3, FUN=median, ...) {

# 加载 LSPM

if(!require(LSPM,quietly=TRUE)) stop(warnings())

# 处理没有负回报的情况

for (sys in 1:numsys) {

if (min(x[,sys])> -1) x[,sys][which.min(x[,sys])]<- -0.03

}

# 用于将数据分箱的函数

quantize <- function(x, n, FUN=median, ...) {

if(is.character(FUN)) FUN <- get(FUN)

bins <- cut(x, n, labels=FALSE)

res <- sapply(1:NROW(x), function(i) FUN(x[bins==bins[i]], ...))

}

# 允许在'x'中的每个系统中使用不同的'n'值

if(NROW(n)==1) {

n <- rep(n,NCOL(x))

} else

if(NROW(n)!=NCOL(x)) stop("invalid 'n'")

# 将数据在'x'中进行分箱

qd <- sapply(1:NCOL(x), function(i) quantize(x[,i],n=n[i],FUN=FUN,...))

# 合并概率

probs <- rep(1/NROW(x),NROW(x))

res <- aggregate(probs, by=lapply(1:NCOL(qd), function(i) qd[,i]), sum)

# 清理输出，返回 lsp 对象

colnames(res) <- colnames(x)

res <- lsp(res[,1:NCOL(x)],res[,NCOL(res)])

返回 res

}

for (i in 0:(numCycles-1)) {

# 定义周期边界

start<-1+(i*wf)

end<-optim+(i*wf)

# 获取优化周期的回报并创建 JPT

# 指定箱子的数量；似乎并不会对结果产生太大影响

numbins<-6

jpt <- jointProbTable(assetROC[start:end,1:numsys],n=rep(numbins,numsys))

outcomes<-jpt[[1]]

probs<-jpt[[2]]

port<-lsp(outcomes,probs)

# DEoptim 参数（参见?DEoptim）

np=numsys*10       #10 * 市场系统数

imax=1000       #最大迭代次数

crossover=0.6       #交叉概率

NR <- NROW(port$f)

DEctrl <- list(NP=np, itermax=imax, CR=crossover, trace=TRUE)

# 优化 f

res <- optimalf(port, control=DEctrl)

#使用 upper 限制到可能感觉舒适的水平

#res <- optimalf(port, control=DEctrl, lower=rep(0,13), upper=rep(0.2,13))

#这些是其他可能性，但我放弃了 24 小时后

#来自 Foss Trading 的 maxProbProfit

#res<-maxProbProfit(port, 1e-6, 6, probDrawdown, 0.1, DD=0.2, control=DEctrl)

#来自 Foss Trading 的 probDrawdown

#res<-optimalf(port,probDrawdown,0.1,DD=0.2,horizon=6,control=DEctrl)

#将杠杆量保存为最佳 f

#《Ralph Vince 杠杆空间交易模型》书中的例子

#所有以美元计价，这让我困惑

#直到我解决了这个问题，我将 lev 行更改为显示最佳 f 输出

lev<-res$f[1:numsys]

#lev<-c(res$f[1]/(-jpt$maxLoss[1]/10),res$f[2]/(-jpt$maxLoss[2]/10))

levmat<-c(rep(1,wf)) %o% lev #以便我们可以与 wfassetROC 相乘

#获取下一个 Walk-Forward 期间的收益

wfassetROC <- assetROC[(end+1):(end+wf),1:numsys]

wflevassetROC <- wfassetROC*levmat #将杠杆应用于收益

if (i==0) fullassetROC<-wflevassetROC else fullassetROC<-rbind(fullassetROC,wflevassetROC)

if (i==0) levered<-levmat else levered<-rbind(levered,levmat)

}

#不是很熟悉 xts，但这会向 levered 添加日期

levered<-xts(levered,order.by=index(fullassetROC) )

colnames(levered)<-c("sp500 最佳 f","crb 最佳 f")

chart.TimeSeries(levered, legend.loc="topleft", cex.legend=0.6)

#回顾最佳 f 值

#我不得不将窗口填充到我的屏幕上，以避免 R 报错边距

par(mfrow=c(numsys,1))

for (i in 1:numsys) {

chart.TimeSeries(levered[,i],xlab=NULL)

}

#charts.PerformanceSummary(fullassetROC, ylog=TRUE, main="应用最佳 f 作为分配的性能摘要")

assetROCAnalyze<-merge(assetROC,fullassetROC)

colnames(assetROCAnalyze)<-c("sp500","crb","US10y","sp500 f","crb f")

charts.PerformanceSummary(assetROCAnalyze,ylog=TRUE,main="应用最佳 f 作为分配的性能摘要")

#建立一个包含 SP500 和 CRB 的投资组合

leveredadjust<-levered

#允许在 CRB 中分配高达 50%

leveredadjust[,2]<-ifelse(levered[,2]<0.25,0,0.5)

#允许在 SP500 中分配高达 100%，但投资组合限制在 1 杠杆

leveredadjust[,1]<-ifelse(levered[,1]<0.25,0,1-levered[,2])

colnames(leveredadjust)<-c("sp500 投资组合分配","crb 投资组合分配")

assetROCadjust<-merge(assetROCAnalyze,leveredadjust[,1:2]*assetROC[,1:2])

colnames(assetROCadjust)<-c("sp500","crb","US10y","sp500 f","crb f","sp500 系统成分","crb 系统成分")

charts.PerformanceSummary(assetROCadjust,ylog=TRUE)

#回顾分配与最佳 f

#我不得不将窗口填充到屏幕以避免 R 中的错误

par(mfrow=c(numsys,1))

for (i in 1:numsys) {

chart.TimeSeries(merge(levered[,i],leveredadjust[,i]),xlab=NULL,legend.loc="topleft",main="")

}

#在标普 500 或商品指数失去时添加债券

assetROCportfolio<-assetROCadjust[,6]+assetROCadjust[,7]+ifelse(leveredadjust[,1]+leveredadjust[,2] >= 1,0,(1-leveredadjust[,1]-leveredadjust[,2])*assetROC[,3])

assetROCadjust<-merge(assetROCAnalyze,assetROCportfolio)

colnames(assetROCadjust)<-c("标普 500","商品指数","美国 10 年期","标普 500 f","商品指数 f","系统投资组合")

charts.PerformanceSummary(assetROCadjust[,c(1:3,6)],ylog=TRUE,main="带债券填充器的最佳 f 系统投资组合")

#请参阅 timelyportfolio 博客文章

[`timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical_6197.html`](http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical_6197.html)

#获取马哈拉诺比斯滤波器的相关性

#从圣路易斯联邦储备(FRED)获取数据，以添加 20 年期美国国债数据

getSymbols("GS20",src="FRED") #加载 20 年期美国国债；20 年期间有间隙 86-93；30 年期在 2000 年代初有间隙

getSymbols("GS30",src="FRED") #加载 30 年期美国国债以填补 20 年期间的空缺 86-93

#用 30 年期填补中止的 20 年期美国国债的空缺

GS20["1987-01::1993-09"]<-GS30["1987-01::1993-09"]

assetROC<-merge(assetROC,momentum(GS20)/100)

corrBondsSp<-runCor(assetROC[,4],assetROC[,1],n=7)

corrBondsCrb<-runCor(assetROC[,4],assetROC[,2],n=7)

corrSpCrb<-runCor(assetROC[,2],assetROC[,1],n=7)

#资产类别之间的相关性的综合测量和 ROC 加权相关性

assetCorr<-(corrBondsSp+corrBondsCrb+corrSpCrb+

(corrBondsSp*corrSpCrb*assetROC[,1])+

(corrBondsCrb*corrSpCrb*assetROC[,2])-

assetROC[,4])/6

#资产类别的 ROC 总和

assetROCSum<-assetROC[,1]+assetROC[,2]+assetROC[,4]

#最后的紊流测量

turbulence<-abs(assetCorr*assetROCSum*100)

colnames(turbulence)<-"紊流-相关性"

signal<-ifelse(turbulence>0.8,0,1)

signal<-lag(signal,k=1)

signal[0]<-0

system_perf_turbulence<-assetROCportfolio*signal

perf_compare<-merge(assetROC[,1:2],assetROCportfolio,system_perf_turbulence)

colnames(perf_compare)<-c("标普 500","商品指数","LSPM 投资组合","LSPM 投资组合 _ 紊流")

charts.PerformanceSummary(perf_compare,ylog=TRUE,colorset=c("gray70","goldenrod","cadetblue","darkolivegreen3"),main="原始 LSPM 系统和紊流 LSPM 系统的比较")

downsideTable<-melt(cbind(rownames(table.DownsideRisk(perf_compare)),table.DownsideRisk(perf_compare))))

colnames(downsideTable)<-c("统计量","投资组合","数值")

ggplot(downsideTable, stat="identity", aes(x=Statistic,y=Value,fill=Portfolio)) + geom_bar(position="dodge") + coord_flip()
