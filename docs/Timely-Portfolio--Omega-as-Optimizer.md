<!--yml

category: 未分类

date: 2024-05-18 15:16:10

-->

# Timely Portfolio: Omega as Optimizer

> 来源：[`timelyportfolio.blogspot.com/2011/05/omega-as-optimizer.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/05/omega-as-optimizer.html#0001-01-01)

在 Jan Straatman 的演示期间，我发了推文。

> Jan Straatman [#cfa2011](http://twitter.com/search?q=%23cfa2011) 在现实生活中没有正态分布，因此使用 Omega 函数来优化实际回报。

在演示结束后，我问了 Jan 在 Omega 之后的第二选择是什么，他回答什么都没有。他补充说他非常不喜欢优化，并且除非绝对必要，否则会避免任何优化。尽管我和他一样不喜欢优化并避免诱惑，但我认为在 R 中玩弄 Omega 可能会提供一个非常有用的例子。

对 Omega 的一个非常基本的使用可能允许相对强势风格的策略来构建股票组合。对于那些不熟悉 Hussman Strategic Growth Fund (HSGFX) 的人，它提供了一种绝对回报风格的股票策略（参见博客文章 [his own drummer](http://rp-pix.com/ep "his own drummer") 和 [The Timing Value of John Hussman’s Market Climate Assessments](http://feedproxy.google.com/~r/cxo/~3/idB_lhY4I2w/)）。随意玩弄其他基金或指数，但我认为我们可以通过投资具有更高 Omega 的投资来构建一个不错的基础组合，只要 Omega 超过 1.5。

投资组合看起来是这样的。

一些关于 Omega 的工作论文可以在 SSRN 上找到。

> [`papers.ssrn.com/sol3/papers.cfm?abstract_id=365740`](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=365740 "http://papers.ssrn.com/sol3/papers.cfm?abstract_id=365740")
> 
> [`papers.ssrn.com/sol3/papers.cfm?abstract_id=1289269`](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1289269 "http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1289269")
> 
> [`papers.ssrn.com/sol3/papers.cfm?abstract_id=910233`](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=910233 "http://papers.ssrn.com/sol3/papers.cfm?abstract_id=910233")
> 
> [`papers.ssrn.com/sol3/papers.cfm?abstract_id=557128&rec=1&srcabs=365740`](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=557128&rec=1&srcabs=365740 "http://papers.ssrn.com/sol3/papers.cfm?abstract_id=557128&rec=1&srcabs=365740")

Jan 不再在 SSRN 上发布他的工作，但这里有一些他较早的工作论文。[`papers.ssrn.com/sol3/cf_dev/AbsByAuth.cfm?per_id=485183`](http://papers.ssrn.com/sol3/cf_dev/AbsByAuth.cfm?per_id=485183 "http://papers.ssrn.com/sol3/cf_dev/AbsByAuth.cfm?per_id=485183") 此外，这里是一篇来自[金融时报](http://www.ft.com/intl/cms/s/0/09500f7c-ecc6-11de-8070-00144feab49a.html#axzz1MXfd7JhS) 的好文章。

R 代码：

require(quantmod)

require(PerformanceAnalytics)

require(ggplot2)

tckr<-c("^GSPC","HSGFX")

#define start and end dates

#Hussman starts 2000 but I use 1990 in case you want to look at other funds

start<-"1990-12-31"

end<- format(Sys.Date(),"%Y-%m-%d") # yyyy-mm-dd

# 拉取从 Yahoo! Finance 调整后的 tckr 指数数据

从 Yahoo! Finance 获取调整后的 tckr 指数数据

# 从每日数据转换到每周数据

GSPC<-to.weekly(GSPC, indexAt='endof')[,4]

HSGFX<-to.weekly(HSGFX, indexAt='endof')[,4]

# 将价格数据转换为用于 PerformanceAnalytics 分析的回报数据

GSPC<-weeklyReturn(GSPC)

HSGFX<-weeklyReturn(HSGFX)

# 合并两个序列

RetToAnalyze<-na.omit(merge(GSPC,HSGFX))

colnames(RetToAnalyze)<-tckr

`#some charts if you want to see them`

`#charts.PerformanceSummary(RetToAnalyze)`

`#charts.RollingRegression(RetToAnalyze[,2,drop=F],RetToAnalyze[,1],width=25,Rf=0,legend.loc="topleft")`

`#chart.RollingPerformance(RetToAnalyze,FUN="Omega",legend.loc="topleft",width=25)`

`#merge the 25-week rolling Omega for the two investements`

signal<-merge(apply.rolling(RetToAnalyze[,1],FUN="Omega",width=25),apply.rolling(RetToAnalyze[,2],FUN="Omega",width=25))

`#lag the data by 1`

signal<-lag(signal,k=1)

signal[is.na(signal)]<-0

`#get return for the investment with higher Omega`

`#use 0 if Omega does not exceed 1.5`

`ret<-ifelse(signal[,1] > signal[,2] & signal[,1]>1.5,RetToAnalyze[,1],ifelse(signal[,2]>1.5,RetToAnalyze[,2],0))`

`#combine investment returns and the omega generated Portfolio`

`returnComparison<-merge(ret,RetToAnalyze)`

colnames(returnComparison)<-c("PortfolioOmega",colnames(RetToAnalyze))

`charts.PerformanceSummary(returnComparison, main="HSGFX and SP500 versus Omega Generated Portfolio",`

colorset=c("cadetblue","gray70","darkolivegreen3"))

`#downside risk comparison`

downsideTable<-melt(cbind(rownames(table.DownsideRisk(returnComparison)),table.DownsideRisk(returnComparison)))

colnames(downsideTable)<-c("Statistic","Portfolio","Value")

`ggplot(downsideTable, stat="identity", aes(x=Statistic,y=Value,fill=Portfolio)) + geom_bar(position="dodge") + coord_flip()`
