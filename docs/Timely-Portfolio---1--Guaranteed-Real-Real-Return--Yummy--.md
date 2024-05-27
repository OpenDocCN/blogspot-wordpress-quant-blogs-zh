<!--yml

分类：未分类

日期：2024-05-18 15:12:21

-->

# 及时组合：-1%保证实际实际收益率！美味？？

> 来源：[`timelyportfolio.blogspot.com/2011/08/1-guaranteed-real-real-return-yummy.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/08/1-guaranteed-real-real-return-yummy.html#0001-01-01)

如果我们正在烹制债券收益，我们有 3 种原料可供选择：通胀、信用和实际。历史上，这个配方看起来像这样（如在[债券收益的历史来源](http://timelyportfolio.blogspot.com/2011/04/historical-sources-of-bond-returns.html)中描述）。

0-5 部分通胀

+ 1-2 部分信用

+ 1-3 部分实际

图表看起来像这样。

在美好的旧时光里，信用风险并不适用于美国国债，但让我们假设在当前情况下，有 1.4%的概率会因信用风险导致 50%的损失（相当于当前 10 年期美国国债的 CDS 价格为 0.70%）。通胀部分不应包括这种信用风险补偿，因此对于没有信用成分的美国国债，这个数字必须包含在实际成分中。当美国 10 年期 TIPS 收益率为 0%，甚至更糟的是上周的-0.25%时，这意味着投资者认为实际实际收益率为-1%是一个美味的食谱。

我认为我需要寻找其他机会。

所有人都可以在[彭博社](http://www.bloomberg.com/apps/quote?ticker=CT786916:IND)获取美国 10 年期 CDS 信息。

R 代码：

```
require(quantmod)
require(PerformanceAnalytics)   getSymbols("GS10",src="FRED") #load 10yTreasury
getSymbols("BAA",src="FRED") #load Corporate for credit
getSymbols("CPIAUCSL",src="FRED") #load CPI for inflation    bondReturnSources<-na.omit(merge(ROC(CPIAUCSL,12,type="discrete")*100,
            BAA-GS10,GS10-ROC(CPIAUCSL,12,type="discrete")*100))
bondReturnSources<-merge(bondReturnSources,
            bondReturnSources[,1]+bondReturnSources[,2]+bondReturnSources[,3]) #add for total
colnames(bondReturnSources)<-c("Inflation","Credit","Real","Total")   chart.TimeSeries(bondReturnSources,legend.loc="bottom",
            main="Historical Sources of Bond Returns",
            ylab="Yield as %",
            colorset=c("darkolivegreen3","cadetblue","goldenrod","gray70"))
```

[由 Pretty 创建](http://www.inside-r.org/pretty-r "由 Pretty R 在 inside-R.org 创建")

[](http://www.inside-r.org/pretty-r "由 Pretty R 在 inside-R.org 创建")
