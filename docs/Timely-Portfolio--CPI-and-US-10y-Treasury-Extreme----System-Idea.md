<!--yml

category: 未分类

date: 2024-05-18 15:17:34

-->

# 及时组合：CPI 和 US 10 年期国债的极端情况 –> 系统想法

> 来源：[`timelyportfolio.blogspot.com/2011/05/cpi-and-us-10y-treasury-extreme-system.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/05/cpi-and-us-10y-treasury-extreme-system.html#0001-01-01)

当我看到极端情况时，我会感到有必要进行探索。美国 10 年期国债收益率与年化的 3 个月 CPI 变化率相比处于极端水平。

当然，我必须尝试围绕这个想法构建一个系统。尽管这个 3 个月的 CPI 变化率为 S&P 500 的进出产生了一个不错的信号，但似乎 6 到 12 个月的变化率效果更好。我们只需使用 US 10 年期国债减去（自 CPI 发布之后的次月中旬）9 个月的 CPI 变化率。如果 9 个月的 S&P 500 变化率超过这个 US10y-9 个月 CPI 率，则进入多头 S&P 500 头寸。

结果比我预期的要好，而且自由度相当稳健。

对于一些事后的优化，我们可以在上行极端情况上加一个退出信号。神奇的是，1987 年的情况消失了。我不建议这种事后优化的方法，除非这个概念在其他多个市场上都行之有效，但上行极端情况也会使您退出 S&P 500。

我用这些只是为了举例说明。我并不提供金融建议。你要对自己的盈亏负责。

R 代码：

require(PerformanceAnalytics)

require(quantmod)

getSymbols("CPIAUCNS",src="FRED") #从联邦储备系统（Fed Fred）加载 CPI

getSymbols("GS10",src="FRED") #从联邦储备系统（Fed Fred）加载 US Treasury 10 年期

getSymbols("GS20",src="FRED") #从联邦储备系统（Fed Fred）加载 US Treasury 20 年期

getSymbols("GS30",src="FRED") #从联邦储备系统（Fed Fred）加载 US Treasury 30 年期

getSymbols("SP500",src="FRED") #从联邦储备系统（Fed Fred）加载 SP500

#使用 30 年期替代 20 年期中断的债券

GS20["1987-01::1993-09"]<-GS30["1987-01::1993-09"]

SP500<-to.monthly(SP500)[,4]

#将格式转换为 yyyy-mm-dd 的月度格式，以每个月的第一天为准

index(SP500)<-as.Date(index(SP500))

#将 CPI 的年化 3 个月变化率从 US 10 年期中减去

US10yMinus3moCPI<-GS10/100-((1+ROC(CPIAUCNS,3))⁴-1)

chartSeries(US10yMinus3moCPI,theme="white.mono")

#获取 CPI 的 12 个月变化率

#将 10 年期国债的滞后金额减去

#我也检索了 20 年的数据，如果您想在这里使用的话

#这没有太大的区别

US10yMinusCPI<-GS10/100-lag(ROC(CPIAUCNS,9,type="discrete"),k=1)

signal<-ifelse(ROC(SP500,n=9)-lag(US10yMinusCPI) > -0.05,1,0)

signal<-lag(signal,k=1)

signal[is.na(signal)]<-0

SPreturn<-ROC(SP500,1,type="discrete")  # 1 个月的 S&P 500 变化率

SPreturn[1]<-0

SystemReturn<-signal*SPreturn

SystemEquity<-cumprod(1+signal*SPreturn)*coredata(SP500)[1]

return_compare<-merge(SystemReturn,SPreturn)

colnames(return_compare)<-c("基于 US10y & CPI 的 SP500 系统","SP500")

charts.PerformanceSummary(return_compare,ylog=TRUE,

main="SP500 和系统的绩效比较",

颜色设置 = c("海军蓝","深橄榄绿 3")

图表系列(系统股权,主题="白色.单色",对数=TRUE,

技术分析="添加技术分析(SP500,开启=1);添加技术分析(ROC(SP500,n=9)-滞后(US10yMinusCPI))"，

名称="SP500 和带信号系统的表现比较")

#现在通过一些事后优化来真正限制回撤

#添加一个极端上升过滤器，1987 年神奇地消失了

#不推荐这种方法，但这是一个好例子

信号 <- ifelse(ROC(SP500,n=9)-滞后(US10yMinusCPI) > -0.05 & ROC(SP500,n=9)-滞后(US10yMinusCPI) < 0.2,1,0)

信号 <- 滞后(信号,k=1)

信号[is.na(信号)]<-0

SP 回报 <- ROC(SP500,1,类型="离散") # 1 个月 SP500 的变化率

SP 回报[1]<-0

系统回报 <- 信号 * SP 回报

系统股权 <- 累积乘积(1+信号 * SP 回报) * SP500 的核心数据[1]

回报比较 <- 合并(系统回报, 回报比较)

回报比较的列名[1]<-"带上升过滤器的系统"

图表.性能摘要(回报比较,对数=TRUE,

主标题="SP500 和带极端上升限制系统的表现比较",

颜色设置 = c("灰色 70","深橄榄绿 3","海军蓝"))
