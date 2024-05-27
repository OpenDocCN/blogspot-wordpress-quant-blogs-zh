<!--yml

类别：未分类

日期：2024-05-18 15:19:00

-->

# 及时投资组合：债券作为赌场游戏第二部分

> 来源：[`timelyportfolio.blogspot.com/2011/04/bond-market-as-casino-game-part-2.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/04/bond-market-as-casino-game-part-2.html#0001-01-01)

在开始第二部分之前，请参阅[债券作为赌场游戏第一部分](http://timelyportfolio.blogspot.com/2011/04/bond-market-as-casino-game-part-1.html)。对于蒙地卡罗随机模拟的纯洁主义者，请忽略我模拟中的一些不重要的技术细节。

为了破坏乐趣，这里就是结论：

> 无论从哪个角度看，美国债券市场一直是一个非常有利可图的游戏，但游戏正在改变，过去的业绩绝不能预测类似的未来回报。请降低你对债券投资的期望。

考虑到自 1980 年以来我们在巴克莱资本美国综合债券指数中经历的概率和平均结果，让我们看看如果我们把债券市场变成一个游戏，并用微软 Excel 在 10,000 个 30 年的游戏中玩会发生什么（对不起 R，我们稍后会用到你）。

结果显示，在最坏的情况下，10,000 次试验仍然能提供 5.6%的年化回报，这显示了这个游戏的吸引力。下面的图表显示了 10,000 次试验中的 200 次（Excel 限制为 255），实际的巴克莱综合指数结果，以及 10,000 次试验的平均值。

最让我感兴趣的是，游戏似乎正在改变，随着实际值接近平均值，变得不那么有利。这在十年期的汇总表中也清晰地显示出来，随着低利率的出现，预期回报减少。

尽管只使用两个桶有助于简化分析，但我们可以使用更多的桶/箱[Ralph Vince 的*杠杆空间交易模型*](http://www.amazon.com/gp/product/0470455950/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&tag=timelyp-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0470455950)以及 Foss Trading 的 R LSPM 包。

无论从哪个角度看，美国债券市场一直是一个非常有利可图的游戏，但游戏正在改变，过去的业绩绝不能预测类似的未来回报。请降低你对债券投资的期望。

R 代码：

#请参阅 au.tra.sy 博客[`www.automated-trading-system.com/`](http://www.automated-trading-system.com/)

#原始代码以及[`www.fosstrading.com`](http://www.fosstrading.com)

#我承认这大部分代码的功劳

#我只是改了几个地方，使用了 xts 返回序列

#以及债券模拟

require(xts)

require(PerformanceAnalytics)

numbins<-10

# 从 csv 文件获取数据序列并限制为 1980 至 2010

rtn<-as.xts(read.csv("lbustruu.csv",row.names=1))["1980::"]

# 计算 WF 周期的数量

numCycles = floor((nrow(rtn)-optim)/wf)

# 定义 JPT 函数

jointProbTable <- function(x, n=3, FUN=median, ...) {

#加载 LSPM

if(!require(LSPM,quietly=TRUE)) stop(warnings())

#用于分箱数据的函数

quantize <- function(x, n, FUN=median, ...) {

if(is.character(FUN)) FUN <- get(FUN)

bins <- cut(x, n, labels=FALSE)

res <- sapply(1:NROW(x), function(i) FUN(x[bins==bins[i]], ...))

}

# 为'x'中的每个系统允许不同的'n'值

if(NROW(n)==1) {

n <- rep(n,NCOL(x))

} else

if(NROW(n)!=NCOL(x)) stop("invalid 'n'")

# 在'x'中进行数据分箱

qd <- sapply(1:NCOL(x), function(i) quantize(x[,i],n=n[i],FUN=FUN,...))

# 汇总概率

probs <- rep(1/NROW(x),NROW(x))

res <- aggregate(probs, by=lapply(1:NCOL(qd), function(i) qd[,i]), sum)

# 清理输出，返回 lsp 对象

colnames(res) <- colnames(x)

res <- lsp(res[,1:NCOL(x)],res[,NCOL(res)])

return(res)

}

# 获取回报率并创建 JPT

jpt <- jointProbTable(rtn,n=numbins)

outcomes<-jpt[[1]]

probs<-jpt[[2]]

port<-lsp(outcomes,probs)

# 分析跌幅

# 使用 LSPM 获取跌幅 > 5% 的概率

drawdownProb<-probDrawdown(port,DD=.05,horizon=12)

# 显示 1 年内 5%跌幅的概率

actualDraw<-sum(table.Drawdowns(rtn)$Length)/NROW(rtn)

# 绘制预期与实际条形图

barplot(rbind(drawdownProb,actualDraw),beside=TRUE,main="预期与实际跌幅 > 5%",names.arg=c("预期", "实际"))

# 分析收益

# 使用 LSPM 获取利润 > 5% 的概率

profitProb<-probProfit(port,target=.05,horizon=12)

# 获取滚动 12 个月回报率

yearReturns<-apply.rolling(rtn,width=12,by=1,FUN="Return.annualized")

# 获取 12 个月回报率实际百分比 > 5%

actualProb<-NROW(yearReturns[which(yearReturns$calcs>.05),1])/NROW(yearReturns)

# 绘制预期与实际条形图

barplot(rbind(profitProb,actualProb),beside=TRUE,main="预期与实际 12 个月 > 5%",names.arg=c("预期", "实际"))
