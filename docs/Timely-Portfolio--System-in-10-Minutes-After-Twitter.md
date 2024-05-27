<!--yml

类别：未分类

日期：2024-05-18 15:11:15

-->

# 及时投资组合：系统在推特后 10 分钟内

> 来源：[`timelyportfolio.blogspot.com/2011/10/system-in-10-minutes-after-twitter.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/10/system-in-10-minutes-after-twitter.html#0001-01-01)

昨晚在推特上，我注意到来自[www.algorithmzoo.com](http://www.algorithmzoo.com)的@milktrader 正在对股票指数进行一些范围研究。我发了一条关于疯狂的罗素 2000 在 7 天内上涨 17%的推文。在 10 分钟内，我发现了一个非常好用的信号。它可能毫无价值，但我想分享一下，以防有人想玩玩它。这不是投资建议，而且可能会损失大量的钱。无论如何，它展示了 R 的威力。

R 代码：

需要(quantmod)

需要(PerformanceAnalytics)

getSymbols("^RUT",from="1896-01-01",to=Sys.Date())

signal<-ifelse(runMax(RUT[,2],7)/runMin(RUT[,3],7)-1-

ROC(RUT[,4],n=20,type="discrete")<0.02,1,0)

perf<-merge(lag(signal,k=1)*ROC(RUT[,4],type="discrete",n=1),

ROC(RUT[,4],type="discrete",n=1))

colnames(perf)<-c("系统","罗素 2000")

charts.PerformanceSummary(perf,ylog=TRUE,

主要内容："快速未测试的罗素 2000 系统")
