<!--yml

category: 未分类

date: 2024-05-18 15:16:01

-->

# Timely Portfolio：BAC ML 和圣路易斯联邦储备银行的礼物

> 来源：[`timelyportfolio.blogspot.com/2011/05/gifts-from-bac-ml-and-federal-reserve.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/05/gifts-from-bac-ml-and-federal-reserve.html#0001-01-01)

美国美林银行和圣路易斯联邦储备银行继续给我带来更多惊喜。 这次，他们添加了历史可追溯到 1998 年的新兴市场债券指数（无法看到 1997-1998 年亚太危机，但可以看到 2001-2002 年的阿根廷危机）。 如果没有昂贵的订阅费用，要获得此类数据是非常困难的。

由于 BAC ML 和联邦储备银行采取了更进一步的措施，我同样感到有义务扩展我的文章 [美国美林银行债券回报来自圣路易斯联邦储备银行](http://timelyportfolio.blogspot.com/2011/05/bank-of-america-merrill-lynch-bond.html) 以包括一些这些新增数据。

R 代码：

#感谢美国美林银行和圣路易斯联邦储备银行提供此数据

require(quantmod)

require(PerformanceAnalytics)

require(ggplot2)

#从圣路易斯联邦储备银行获取美国美林银行债券指数数据

#使用 auto.assign = FALSE 以便我们可以使用较短的名称

MLAsiaEmCorp<-getSymbols("BAMLEMRACRPIASIATRIV",src="FRED",auto.assign=FALSE)

MLLatAmEmCorp<-getSymbols("BAMLEMRLCRPILATRIV", src="FRED", auto.assign=FALSE)

MLUSCorp<-getSymbols("BAMLCC0A0CMTRIV", src="FRED", auto.assign=FALSE)

MLBondIndexes<-na.omit(merge(ROC(MLAsiaEmCorp,1,type="discrete"),ROC(MLLatAmEmCorp,1,type="discrete"),ROC(MLUSCorp,1,type="discrete")))

colnames(MLBondIndexes)<-c("BAC ML 亚洲新兴企业","BAC ML 拉丁美洲新兴企业","BAC ML 美国企业总集")

charts.PerformanceSummary(MLBondIndexes,ylog=TRUE,

colorset=c("军校蓝","深橄榄绿 3","灰色 70"),

main="美国美林银行债券指数来自圣路易斯联邦储备银行")

#对月度回报进行一些风险分析

MLBondIndexes<-merge(monthlyReturn(MLAsiaEmCorp),monthlyReturn(MLLatAmEmCorp),monthlyReturn(MLUSCorp))

colnames(MLBondIndexes)<-c("BAC ML 亚洲新兴企业","BAC ML 拉丁美洲新兴企业","BAC ML 美国企业总集")

downsideTable<-melt(cbind(rownames(table.DownsideRisk(MLBondIndexes)),table.DownsideRisk(MLBondIndexes))))

colnames(downsideTable)<-c("统计","债券指数","数值")

ggplot(downsideTable, stat="identity", aes(x=统计,y=数值,fill=债券指数)) + geom_bar(position="dodge") + coord_flip()

#ggplot 年度回报

yearReturns<-na.omit(table.CalendarReturns(MLBondIndexes)[,(13:NCOL(table.CalendarReturns(MLBondIndexes)))])

yearReturns<-melt(cbind(rownames(yearReturns),yearReturns))

colnames(yearReturns)<-c("年份","债券指数","回报")

ggplot(yearReturns, stat="identity", aes(x=年份,y=回报,fill=债券指数)) + geom_bar(position="dodge")

#ggplot CAPM 统计

capmTable<-melt(cbind(rownames(table.CAPM(MLBondIndexes[,1:2],MLBondIndexes[,3])),table.CAPM(MLBondIndexes[,1:2],MLBondIndexes[,3])))

`colnames(capmTable)<-c("Statistic","BondIndex","Return")`

`ggplot(capmTable, stat="identity", aes(x=Statistic,y=Return,fill=BondIndex)) + geom_bar(position="dodge") + coord_flip()`
