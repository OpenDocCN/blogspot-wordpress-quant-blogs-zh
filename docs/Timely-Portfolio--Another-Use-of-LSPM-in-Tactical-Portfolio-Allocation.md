<!--yml

类别：未分类

日期：2024-05-18 15:17:50

-->

# 及时投资组合：LSPM 在战术投资组合分配中的另一种应用

> 来源：[`timelyportfolio.blogspot.com/2011/04/another-use-of-lspm-in-tactical.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/04/another-use-of-lspm-in-tactical.html#0001-01-01)

在[Ralph Vince 的杠杆空间交易模型](http://timelyportfolio.blogspot.com/2011/04/slightly-different-use-of-ralph-vinces.html)的稍微不寻常使用之后，我认为我应该跟进一些更接近我对 Ralph Vince 书籍的解释的内容。

LSPM 似乎在投资组合分配问题中表现良好。在这个战术分配系统中，我将使用 R 中 LSPM 包生成的最优 f 来构建包含 SP500、美国 10 年和 CRB 的投资组合。如果我们使用最优 f 作为对 SP500 和 CRB 的分配，那么结果看起来像这样。

总的来说，我最大的问题是在整个投资组合中应用我的系统。组成部分很简单，但是融合很麻烦。如果我应用基本的方法对 SP500 和 CRB 进行月度再平衡，我会得到这样东西（不使用任何杠杆）。

SP500 组成部分有所改善，但由于我对更倾向于回归均值的 CRB 设定了 50%的限制，CRB 组成部分的表现不及直接最优的 f 分配。

由于大多数客户不喜欢现金，当分配完 CRB 和 SP500 后还有剩余空间时，我们可以用债券填满投资组合。整个套餐看起来像这样。

正如我之前的所有帖子一样，我希望我的帖子能激发讨论和思考。这里的回撤比我希望的要严重得多。请告诉我您如何改进这个系统。

R 代码：

#请参阅 au.tra.sy 博客[`www.automated-trading-system.com/`](http://www.automated-trading-system.com/)

#原始前进/优化代码和[`www.fosstrading.com`](http://www.fosstrading.com)

#用于其他技术

要求（PerformanceAnalytics）

要求（quantmod）

要求（RQuantLib）

#获取债券回报以避免专有数据问题

#请参阅之前的 timelyportfolio 博客文章，以了解解释

#可能需要将其制成函数，因为我将大量使用

获取符号("GS10"，来源="FRED") #从美联储弗雷德加载美国国债 10 年

GS10pricereturn<-GS10 #设置此符号以持有价格回报

GS10pricereturn[1,1]<-0

colnames(GS10pricereturn)<-"PriceReturn"

#我知道我需要将此内容向量化，但还不够资格

#请随意留言，告诉我如何做到这一点

对于（i 在 1:（NROW(GS10)-1））{

GS10pricereturn[i+1,1]<-FixedRateBondPriceByYield(yield=GS10[i+1,1]/100,issueDate=Sys.Date(),

到期日= advance("UnitedStates/GovernmentBond", Sys.Date(), 10, 3),

rates=GS10[i,1]/100,period=2)[1]/100-1

}

#利息回报将是收益率/12 的一个月

GS10interestreturn<-lag(GS10,k=1)/12/100

colnames(GS10interestreturn)<-"Interest Return"

#总回报将是价格回报+利息回报

GS10totalreturn<-GS10pricereturn+GS10interestreturn

`colnames(GS10totalreturn)<-"Bond Total Return"`

# 从 FRED 获取 sp500 收益率

`getSymbols("SP500",src="FRED")` # 加载 SP500

# 不幸的是，无法替代专有的 CRB 数据

# 从 csv 文件获取数据系列

`CRB<-as.xts(read.csv("spxcrbndrbond.csv",row.names=1))[,2]`

#对数据进行一些操作，以便按月份排列数据

`GS10totalreturn<-to.monthly(GS10totalreturn)[,4]`

`SP500<-to.monthly(SP500)[,4]`

# 将月份格式化为 yyyy-mm-dd，第一天为月初

`index(SP500)<-as.Date(index(SP500))`

#我的 CRB 数据是每月末; 可以改变但在 R 中更有趣

`CRB<-to.monthly(CRB)[,4]`

`index(CRB)<-as.Date(index(CRB))`

#现在让我们合并以获取资产类别回报

`assetROC<-na.omit(merge(ROC(SP500,type="discrete"),CRB,GS10totalreturn))`

# 设置 Walk-Forward 参数（周期数）

`optim<-12` #1 年 = 12 个月收益率

`wf<-1` #每月向前行走 1 步

`numsys<-2`

# 计算 WF 周期数

`numCycles = floor((nrow(assetROC)-optim)/wf)`

# 定义 JPT 函数

# 现在这是 LSPM 包的一部分，但是当没有负回报时会失败

# 因此我仍然在这里包括可以强制负回报的内容

`jointProbTable <- function(x, n=3, FUN=median, ...) {`

# 加载 LSPM

如果（`!require(LSPM,quietly=TRUE)`）则停止（警告）

# 处理没有负回报的情况

对于 `sys` 中的每个系统 {

如果（`min(x[,sys])> -1`）`x[,sys][which.min(x[,sys])]<- -0.03`

}

# 将数据进行分组的函数

`quantize <- function(x, n, FUN=median, ...) {`

如果（`is.character(FUN)`）`FUN <- get(FUN)`

`bins <- cut(x, n, labels=FALSE)`

`res <- sapply(1:NROW(x), function(i) FUN(x[bins==bins[i]], ...))`

}

# 允许在 'x' 中的每个系统中使用不同的 'n' 值

如果（`NROW(n)==1`）{

`n <- rep(n,NCOL(x))`

} else

如果 `n` 的行数不等于 `x` 的列数，则停止（"invalid 'n'"）。

# 将 'x' 中的数据进行分组

`qd <- sapply(1:NCOL(x), function(i) quantize(x[,i],n=n[i],FUN=FUN,...))`

# 聚合概率

`probs <- rep(1/NROW(x),NROW(x))`

`res <- aggregate(probs, by=lapply(1:NCOL(qd), function(i) qd[,i]), sum)`

# 清理输出，返回 lsp 对象

`colnames(res) <- colnames(x)`

`res <- lsp(res[,1:NCOL(x)],res[,NCOL(res)])`

`return(res)`

}

对于 `i` 在 `0:(numCycles-1)` 之间 {

# 定义周期边界

`start<-1+(i*wf)`

`end<-optim+(i*wf)`

# 获取优化周期的收益率并创建 JPT

# 指定箱数; 看起来不会对结果产生重大影响

`numbins<-6`

`jpt <- jointProbTable(assetROC[start:end,1:numsys],n=rep(numbins,numsys))`

`outcomes<-jpt[[1]]`

`probs<-jpt[[2]]`

`port<-lsp(outcomes,probs)`

# DEoptim 参数（参见?DEoptim）

`np=numsys*10`       # 10 * mktsys 的数量

`imax=1000`       # 最大迭代次数

`crossover=0.6`       # 交叉概率

`NR <- NROW(port$f)`

`DEctrl <- list(NP=np, itermax=imax, CR=crossover, trace=TRUE)`

# 优化 f

`res <- optimalf(port, control=DEctrl)`

# 使用 upper 来限制到您可能感到舒适的水平

#res <- optimalf(port, control=DEctrl, lower=rep(0,13), upper=rep(0.2,13))

# 这些是其他可能性，但我在 24 小时后放弃了

#来自 Foss Trading 的 maxProbProfit

#res<-maxProbProfit(port, 1e-6, 6, probDrawdown, 0.1, DD=0.2, control=DEctrl)

#来自 Foss Trading 的 probDrawdown

#res<-optimalf(port,probDrawdown,0.1,DD=0.2,horizon=6,control=DEctrl)

# 将杠杆金额保存为最优 f

# 书中的例子 Ralph Vince Leverage Space Trading Model

# 全部以美元为单位，这让我感到困惑

# 直到我解决了将 Lev 线变更为显示最优 f 输出为止

lev<-res$f[1:numsys]

#lev<-c(res$f[1]/(-jpt$maxLoss[1]/10),res$f[2]/(-jpt$maxLoss[2]/10))

levmat<-c(rep(1,wf)) %o% lev #这样我们就可以与 wfassetROC 相乘

# 获取下一个 Walk-Forward 期间的收益

wfassetROC <- assetROC[(end+1):(end+wf),1:numsys]

wflevassetROC <- wfassetROC*levmat #将杠杆应用于收益

if (i==0) fullassetROC<-wflevassetROC else fullassetROC<-rbind(fullassetROC,wflevassetROC)

if (i==0) levered<-levmat else levered<-rbind(levered,levmat)

}

#对 xts 不是很熟悉，但这会给 levered 添加日期

levered<-xts(levered,order.by=index(fullassetROC) )

colnames(levered)<-c("sp500 最优 f","crb 最优 f")

chart.TimeSeries(levered, legend.loc="topleft", cex.legend=0.6)

#审查最优 f 值

#我必须将窗口填满到屏幕上，以避免 R 报错边距

par(mfrow=c(numsys,1))

for (i in 1:numsys) {

chart.TimeSeries(levered[,i],xlab=NULL)

}

#charts.PerformanceSummary(fullassetROC, ylog=TRUE, main="Performance Summary with Optimal f Applied as Allocation")

assetROCAnalyze<-merge(assetROC,fullassetROC)

colnames(assetROCAnalyze)<-c("sp500","crb","US10y","sp500 f","crb f")

charts.PerformanceSummary(assetROCAnalyze,ylog=TRUE,main="Performance Summary with Optimal f Applied as Allocation")

#建立一个包含 SP500 和 CRB 的投资组合

leveredadjust<-levered

#允许 CRB 的分配高达 50%

leveredadjust[,2]<-ifelse(levered[,2]<0.25,0,0.5)

#允许在 SP500 中分配高达 100%，但投资组合受到 1 倍杠杆的限制

leveredadjust[,1]<-ifelse(levered[,1]<0.25,0,1-levered[,2])

colnames(leveredadjust)<-c("sp500 投资组合分配","crb 投资组合分配")

assetROCadjust<-merge(assetROCAnalyze,leveredadjust[,1:2]*assetROC[,1:2])

colnames(assetROCadjust)<-c("sp500","crb","US10y","sp500 f","crb f","sp500 系统组件","crb 系统组件")

charts.PerformanceSummary(assetROCadjust,ylog=TRUE)

#审查分配与最优 f

# 我必须将窗口填满到屏幕上，以避免 R 报错边距

par(mfrow=c(numsys,1))

for (i in 1:numsys) {

chart.TimeSeries(merge(levered[,i],leveredadjust[,i]),xlab=NULL,legend.loc="topleft",main="")

}

# 当脱离 SP500 或 CRB 时添加债券

assetROCportfolio<-assetROCadjust[,6]+assetROCadjust[,7]+ifelse(leveredadjust[,1]+leveredadjust[,2] >= 1,0,(1-leveredadjust[,1]-leveredadjust[,2])*assetROC[,3])

assetROCadjust<-merge(assetROCAnalyze,assetROCportfolio)

colnames(assetROCadjust)<-c("sp500","crb","US10y","sp500 f","crb f","系统投资组合")

charts.PerformanceSummary(assetROCadjust[,c(1:3,6)],ylog=TRUE,main="Optimal f System Portfolio with Bond Filler")
