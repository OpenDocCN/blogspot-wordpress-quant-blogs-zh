<!--yml

类别：未分类

日期：2024-05-18 15:19:24

-->

# Timely Portfolio：R 中免费且易用的货币监控

> 来源：[`timelyportfolio.blogspot.com/2011/03/free-and-easy-currency-monitor-in-r.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/03/free-and-easy-currency-monitor-in-r.html#0001-01-01)

虽然这不是跟踪货币的最佳方式，但是在 R 中监控货币的工作变得越来越重要，并且可以免费且轻松地使用美国联邦储备委员会 FRED 数据。 可以使用 [此处列出的符号](http://research.stlouisfed.org/fred2/categories/94) 调整为您喜欢的货币。 

参见我的上一篇帖子，了解如何便宜、简单地监控[潜在的美元崩溃](http://timelyportfolio.blogspot.com/2011/03/death-spiral-warning-graph.html)。 另外，货币再次变得重要，因此在投资时不要忽视它们。 不要说我没有警告过你，也不要借口说你没有昂贵的装备。

R 代码：

require(quantmod)

require(PerformanceAnalytics)

#从美国联邦储备委员会 FRED 数据系列获取亚洲货币数据

getSymbols("DEXKOUS",src="FRED") #加载韩国数据

getSymbols("DEXMAUS",src="FRED") #加载马来西亚数据

getSymbols("DEXSIUS",src="FRED") #加载新加坡数据

getSymbols("DEXTAUS",src="FRED") #加载台湾数据

getSymbols("DEXCHUS",src="FRED") #加载中国数据

getSymbols("DEXJPUS",src="FRED") #加载日本数据

getSymbols("DEXTHUS",src="FRED") #加载泰国数据

getSymbols("DEXBZUS",src="FRED") #加载巴西数据

getSymbols("DEXMXUS",src="FRED") #加载墨西哥数据

getSymbols("DEXINUS",src="FRED") #加载印度数据

getSymbols("DTWEXO",src="FRED") #加载其他美元交易伙伴数据

getSymbols("DTWEXB",src="FRED") #加载美元综合数据

par(mfrow=c(3, 4)) #为图表提供 3 行 4 列

plot(1/coredata(DEXKOUS["1995::2011"]),type="l",ylab="韩国")

plot(1/coredata(DEXMAUS["1995::2011"]),type="l",ylab="马来西亚")

plot(1/coredata(DEXSIUS["1995::2011"]),type="l",ylab="新加坡")

plot(1/coredata(DEXTAUS["1995::2011"]),type="l",ylab="台湾")

plot(1/coredata(DEXCHUS["1995::2011"]),type="l",ylab="中国")

plot(1/coredata(DEXJPUS["1995::2011"]),type="l",ylab="日本")

plot(1/coredata(DEXTHUS["1995::2011"]),type="l",ylab="泰国")

plot(1/coredata(DEXBZUS["1995::2011"]),type="l",ylab="巴西")

plot(1/coredata(DEXMXUS["1995::2011"]),type="l",ylab="墨西哥")

plot(1/coredata(DEXINUS["1995::2011"]),type="l",ylab="印度")

plot(coredata(DTWEXO["1995::2011"]),type="l",ylab="其他美元")

plot(coredata(DTWEXB["1995::2011"]),type="l",ylab="美元综合")

#如果您更喜欢漂亮的图表，可以使用

chartSeries(to.monthly(1/DEXSIUS),theme = chartTheme("white"),name="新加坡元/美元",TA="addBBands(10)")
