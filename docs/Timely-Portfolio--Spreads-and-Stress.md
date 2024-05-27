<!--yml

category: 未分类

日期：2024 年 05 月 18 日 15 时 15 分 53 秒

-->

# Timely Portfolio: 利差和压力

> 来源：[`timelyportfolio.blogspot.com/2011/05/spreads-and-stress.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/05/spreads-and-stress.html#0001-01-01)

由于我们有来自 BAC ML 和联邦储备系统的[礼物](http://timelyportfolio.blogspot.com/2011/05/gifts-from-bac-ml-and-federal-reserve.html)，我想我应该再看看债券的另一个有趣的元素。 债券利差作为金融稳定和信心的非常强大的象征。 圣路易斯联邦压力指数是每周更新的，但也许我们可以将利差作为压力或类似于[彭博金融条件指数（BFCIUS）](http://www.bloomberg.com/apps/quote?ticker=BFCIUS:IND)的每日金融不稳定性的代理，这在 [`www.ssc.wisc.edu/~mchinn/fcw_sep112009.pdf`](http://www.ssc.wisc.edu/~mchinn/fcw_sep112009.pdf) 和 [www.princeton.edu/~mwatson/papers/MPF_paper_April_13.pdf](http://www.princeton.edu/~mwatson/papers/MPF_paper_April_13.pdf) 中有很好的解释。

如果我们绘制 BAC ML 新兴市场和高收益利差以及圣路易斯联邦指数的值，很难区分这些线条。

只是为了满足 ggplot2 的粉丝

总体和滚动相关性如下所示。

像波动性和[金融动荡](http://timelyportfolio.blogspot.com/

而且，只是为了好玩，这是一个高阶时刻的图表。

如果你想挑战一下，可以将这些利差数据与我的帖子[Wonderful New Blog TimeSeriesIreland](http://timelyportfolio.blogspot.com/2011/05/wonderful-new-blog-timeseriesireland.html)或[Great FAJ Article on Statistical Measure of Financial Turbulence Part 3](http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical_6197.html)联系起来。 在周末之前，我不认为我有这个能力。

R 代码：

#感谢美国银行美林和圣路易斯联邦提供的这些数据

require(quantmod)

require(PerformanceAnalytics)

require(ggplot2)

#从圣路易斯联邦获取美国银行美林债券指数数据

#使用 auto.assign = FALSE，以便我们可以使用更短的名称

MLEmCorpSpreads<-getSymbols("BAMLEMCBPIOAS",src="FRED",auto.assign=FALSE)

MLHYCorpSpreads<-getSymbols("BAMLH0A0HYM2",src="FRED",auto.assign=FALSE)

getSymbols("STLFSI",src="FRED")  #获取圣路易斯联邦压力指数

spreadsStress<-na.omit(merge(MLEmCorpSpreads,MLHYCorpSpreads,STLFSI))

colnames(spreadsStress)<-c("BAC ML Emerging","BAC ML HY","St Louis Fed Stress")

chart.TimeSeries(spreadsStress,colorset=c("cadetblue","darkolivegreen3","gray70"),

legend.loc="topleft",

main="美国银行美林债券利差和圣路易斯联邦压力指数")

#图表显示利差和压力的变化

spreadsStress<-na.omit(merge(momentum(MLEmCorpSpreads,5),momentum(MLHYCorpSpreads,5),momentum(STLFSI,1)))

colnames(spreadsStress)<-c("BAC ML Emerging","BAC ML HY","St Louis Fed Stress")

chart.TimeSeries(spreadsStress,colorset=c("cadetblue","darkolivegreen3","gray70"),

legend.loc="topleft",

main="美国银行美林证券债券利差和圣路易斯联储压力指数")

#为 ggplot 爱好者

spreadsStressDf<-data.frame(index(spreadsStress),coredata(spreadsStress))

colnames(spreadsStressDf)<-c("Date",colnames(spreadsStress))

spreadsStressDf<-melt(spreadsStressDf,id.var="Date")

colnames(spreadsStressDf)<-c("Date","Index","Value")

ggplot(spreadsStressDf, stat="identity", aes(x=Date,y=Value,colour=Index)) + geom_line() +

scale_x_date(format = "%Y") +

opts(title = "美国银行美林证券债券利差和圣路易斯联储压力指数")

#图表相关性

chart.Correlation(spreadsStress,main="美国银行美林证券债券利差和圣路易斯联储压力指数相关性")

#探索自相关延迟

par(mfrow=c(3,1))  #3 行 1 列

acf(spreadsStress[,1],main=colnames(spreadsStress)[1])

acf(spreadsStress[,2],main=colnames(spreadsStress)[2])

acf(spreadsStress[,3],main=colnames(spreadsStress)[3])

#获取滚动相关性

corHYStress<-runCor(spreadsStress[,3],spreadsStress[,1],n=20)

corEmStress<-runCor(spreadsStress[,3],spreadsStress[,2],n=20)

corAll<-merge(corHYStress,corEmStress)

chart.TimeSeries(corAll,main="滚动 20 周的利差和压力指数相关性",

legend.loc="topright", colorset=c("cadetblue","darkolivegreen3"))

#查看高阶矩

higherMoments<-table.HigherMoments(spreadsStress[,1:2],spreadsStress[,3])

higherMoments<-melt(cbind(rownames(higherMoments),higherMoments))

colnames(higherMoments)<-c("Moment","Index","Value")

ggplot(higherMoments, stat="identity", aes(x=Moment,y=Value,fill=Index)) +

geom_bar(position="dodge") + coord_flip() +

opts(legend.position=c(.75,0.88)) #感谢 timeseriesireland 的提示
