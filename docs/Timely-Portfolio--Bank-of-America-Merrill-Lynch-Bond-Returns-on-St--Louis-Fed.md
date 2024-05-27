<!--yml

category: 未分类

date: 2024-05-18 15:16:54

-->

# Timely Portfolio: Bank of America Merrill Lynch Bond Returns on St. Louis Fed

> 来源：[`timelyportfolio.blogspot.com/2011/05/bank-of-america-merrill-lynch-bond.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/05/bank-of-america-merrill-lynch-bond.html#0001-01-01)

尽管我抱怨过专有数据，但圣路易斯联邦储备银行今天宣布了[在其 FRED 网站上提供美国银行梅隆债券指数](http://research.stlouisfed.org/fred2/release?rid=209&filter%5B0%5D=units&filter%5B1%5D=Index)。这些数据在范围和持续时间上有限，但通过 R 语言的获取尤其令人赞叹。感谢一些人——美国银行和联邦储备银行。

我将用美国银行公司主债券指数和高级债券指数做一个简短的示例。

我真的很兴奋地想弄清楚这个 PerformanceAnalytics 表格的 ggplot2，所以这里为那些可能在之前的帖子中没有看到这个技巧的人提供另外两个例子。

每次我看到债券指数，我都会对它们惊人的 30 年走势感到惊讶。BAC ML Corporate Master 的 2 个下跌年和 12 个上涨年真正令我惊叹。关于债券这 30 年的牛市走势，请参见我之前的帖子。

R 代码：

#感谢美国银行梅隆和圣路易斯联邦提供这些数据

require(quantmod)

require(PerformanceAnalytics)

require(ggplot2)

#从圣路易斯联邦获取美国银行梅隆债券指数数据

#使用 auto.assign = FALSE，这样我们可以使用更短的名字

MLCorpMaster<-getSymbols("BAMLCC0A0CMTRIV", src="FRED", auto.assign=FALSE)

MLHYMaster<-getSymbols("BAMLHYH0A0HYM2TRIV", src="FRED", auto.assign=FALSE)

MLBondIndexes<-na.omit(merge(ROC(MLCorpMaster, 1, type="discrete"), ROC(MLHYMaster, 1, type="discrete")))

colnames(MLBondIndexes)<-c("BAC ML Corporate Master", "BAC ML High Yield Master II")

charts.PerformanceSummary(MLBondIndexes, ylog=TRUE,

colorset=c("cadetblue", "darkolivegreen3"),

main="来自圣路易斯联邦的 Bank of America Merrill Lynch 债券指数"

#对月回报进行一些下行分析

MLBondIndexes<-merge(monthlyReturn(MLCorpMaster),monthlyReturn(MLHYMaster))

colnames(MLBondIndexes)<-c("BAC ML Corporate Master", "BAC ML High Yield Master II")

downsideTable<-melt(cbind(rownames(table.DownsideRisk(MLBondIndexes)), table.DownsideRisk(MLBondIndexes)))

colnames(downsideTable)<-c("Statistic", "BondIndex", "Value")

ggplot(downsideTable, stat="identity", aes(x=Statistic, y=Value, fill=BondIndex)) + geom_bar(position="dodge") + coord_flip()

yearReturns<-na.omit(table.CalendarReturns(MLBondIndexes)[, (13:NCOL(table.CalendarReturns(MLBondIndexes)))])

yearReturns<-melt(cbind(rownames(yearReturns), yearReturns))

colnames(yearReturns)<-c("Year", "BondIndex", "Return")

ggplot(yearReturns, stat="identity", aes(x=Year, y=Return, fill=BondIndex)) + geom_bar(position="dodge")
