<!--yml

category: 未分类

日期：2024-05-18 15:17:55

-->

# Timely Portfolio：对 Ralph Vince 的杠杆空间交易模型稍微不同的使用

> 来源：[`timelyportfolio.blogspot.com/2011/04/slightly-different-use-of-ralph-vinces.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/04/slightly-different-use-of-ralph-vinces.html#0001-01-01)

为了纪念两天前的新闻稿[Dow Jones Indexes To Develop, Co-Brand Index Family With LSP Partners](http://press.djindexes.com/index.php/dow-jones-indexes-to-develop-co-brand-index-family-with-lsp-partners/)，我想展示 Ralph Vince 的 *杠杆空间交易模型* 的另一种略微不同的用法。

使用 R LSPM 包，我们可以围绕 probProfit 计算构建一个月度系统。这个特定的系统在短期（12 个月）的 probProfit 超过长期（36 个月）的 probProfit 时进入多头。当短期低于长期时退出。

随意替换任何指数。一些我喜欢的是德国 Dax GDAXI，日本 Nikkei N225，韩国 Kospi KS11 和新加坡 Straits Times STI 进行国际测试。额外的美国测试可能会考虑 NDX、RUT、CYC、XBD、HGX、REI、DJUSBK、OSX 或任何您可以想到的内容来进行测试。

结果并不太好，但可观的回撤减少是不错的。请告诉我您如何改进。

R 代码：

#请参见 au.tra.sy 博客 [`www.automated-trading-system.com/`](http://www.automated-trading-system.com/)

#for original code and [`www.fosstrading.com`](http://www.fosstrading.com) for some of the

#其他技术

require(PerformanceAnalytics)

require(PApages)

require(quantmod)

require(LSPM)

tckr<-"^GSPC"

start<-"1929-01-01"

end<- format(Sys.Date(),"%Y-%m-%d") # yyyy-mm-dd

# 从雅虎金融获取 tckr 指数数据

getSymbols(tckr, from=start, to=end)

GSPC<-adjustOHLC(GSPC,use.Adjusted=T)

GSPC<-to.monthly(GSPC)

rtn<-monthlyReturn(GSPC[,4])

# 定义 JPT 函数

jointProbTable <- function(x, n=3, FUN=median, ...) {

# 处理没有负回报的情况；使用 -0.01

for (sys in 1:numsys) {

if (min(x[,sys])> -1) x[,sys][which.min(x[,sys])]<- -0.01

}

# 函数用于对数据进行分组

quantize <- function(x, n, FUN=median, ...) {

if(is.character(FUN)) FUN <- get(FUN)

bins <- cut(x, n, labels=FALSE)

res <- sapply(1:NROW(x), function(i) FUN(x[bins==bins[i]], ...))

}

# 允许对 'x' 中的每个系统的 'n' 使用不同的值

if(NROW(n)==1) {

n <- rep(n,NCOL(x))

} else

if(NROW(n)!=NCOL(x)) stop("invalid 'n'")

# 对 'x' 中的数据进行分组

qd <- sapply(1:NCOL(x), function(i) quantize(x[,i],n=n[i],FUN=FUN,...))

# 聚合概率

probs <- rep(1/NROW(x),NROW(x))

res <- aggregate(probs, by=lapply(1:NCOL(qd), function(i) qd[,i]), sum)

# 清理输出，返回 lsp 对象

colnames(res) <- colnames(x)

res <- lsp(res[,1:NCOL(x)],res[,NCOL(res)])

return(res)

}

# 我知道有更漂亮的方法来完成

# 但我必须在我的限制范围内生活

numsys<-1

numbins<-12

# 设置短期的前进步数（期数）

优化<-9 # 9 个月收益

wf<-1 #向前走 1 个月；我们将单独设置地平线

# 计算 WF 周期数

numCycles = floor((nrow(rtn)-optim)/wf)

for (i in 0:(numCycles-1)) {

# 定义周期边界

start<-1+(i*wf)

end<-optim+(i*wf)

# 获取优化周期的收益并创建 JPT

jpt <- jointProbTable(rtn[start:end,1:numsys],n=rep(numbins,numsys))

outcomes<-jpt[[1]]

probs<-jpt[[2]]

port<-lsp(outcomes,probs)

profitProb<-probProfit(port,target=0,horizon=6)

profitProbWF<-c(rep(1,wf)) %o% profitProb

maxLossWF<-c(rep(1,wf)) %o% jpt$maxLoss

# 创建 xts

profitProbWF<-xts(profitProbWF,order.by=index(rtn[(end+1):(end+wf)]))

maxLossWF<-xts(maxLossWF,order.by=index(rtn[(end+1):(end+wf)]))

if (i==0) profitProbHistory<-profitProbWF else profitProbHistory<-rbind(profitProbHistory,profitProbWF)

if (i==0) maxLossHistory<-maxLossWF else maxLossHistory<-rbind(maxLossHistory,maxLossWF)

}

# 设置长期步行前进参数（周期数）

优化<-30 # 30 个月收益

wf<-1 #向前走 1 个月；我们将单独设置地平线

# 计算 WF 周期数

numCycles = floor((nrow(rtn)-optim)/wf)

for (i in 0:(numCycles-1)) {

# 定义周期边界

start<-1+(i*wf)

end<-optim+(i*wf)

# 获取优化周期的收益并创建 JPT

jpt <- jointProbTable(rtn[start:end,1:numsys],n=rep(numbins,numsys))

outcomes<-jpt[[1]]

probs<-jpt[[2]]

port<-lsp(outcomes,probs)

profitProb<-probProfit(port,target=0,horizon=3)

profitProbWF<-c(rep(1,wf)) %o% profitProb

maxLossWF<-c(rep(1,wf)) %o% jpt$maxLoss

# 创建 xts

profitProbWFlong<-xts(profitProbWF,order.by=index(rtn[(end+1):(end+wf)]))

maxLossWFlong<-xts(maxLossWF,order.by=index(rtn[(end+1):(end+wf)]))

if (i==0) profitProbHistorylong<-profitProbWFlong else profitProbHistorylong<-rbind(profitProbHistorylong,profitProbWFlong)

if (i==0) maxLossHistorylong<-maxLossWFlong else maxLossHistorylong<-rbind(maxLossHistorylong,maxLossWFlong)

}

signalshortterm<-profitProbHistory

# 调整长期最大损失，希望降低回撤

signallongterm<-profitProbHistorylong - maxLossHistorylong

chartSeries(signalshortterm,TA="addTA(signallongterm,on=1)", theme="white", name="短期和长期盈利概率")

# 创建信号，并在长期<短期时进入

sigup <- ifelse(signallongterm < signalshortterm,1,0)

# 不需要滞后，因为信号是从以前的月份生成的]

# sigup <- lag(sigup,1) # 注意 k=1 意味着向前移动

# 用无位置替换缺失的信号

# （通常仅在系列开头）

sigup[is.na(sigup)] <- 0

# 计算资产曲线

eq_up <- cumprod(1+(rtn)*sigup)

perf_compare<-merge(sigup*rtn,rtn[(optim+1):NROW(rtn)])

colnames(perf_compare)<-c("LSPM probProfit 系统",tckr)

charts.PerformanceSummary(perf_compare,ylog=TRUE,legend.loc="topleft",main="LSPM probProfit 系统性能比较")
