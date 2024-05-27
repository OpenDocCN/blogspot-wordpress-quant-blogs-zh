<!--yml

分类：未分类

日期：2024-05-18 15:12:09

-->

# 及时投资组合：跌幅可视化补充

> 来源：[`timelyportfolio.blogspot.com/2011/08/drawdown-visualization-supplement.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/08/drawdown-visualization-supplement.html#0001-01-01)

正如在[跌幅可视化](http://timelyportfolio.blogspot.com/2011/08/drawdown-visualization.html)中所评论的，

> “此外，看看`chart.Event`中的示例，以另一种方式可视化跌幅，这里是指将它们堆叠起来进行比较。”

性能分析包提供了一个非常有助于我们了解跌幅路径的视角，我们可以将其应用于金融和经济时间序列。以下是应用于道琼斯工业平均指数自 1896 年以来的结果。

1929-1954 这段期间确实让这个图表显得混乱，所以让我们把复苏期限制在 750 天内，以获得更好的可视化效果。

我认为将这个例子应用到 GDP 序列上会更有趣。这可以扩展到各种有趣的经济学数据——首先在我脑海中的是工业生产和消费者支出。

R 代码（点击从谷歌文档下载）：

```
require(quantmod)
require(PerformanceAnalytics)   getSymbols("DJIA",src="FRED")
getSymbols("DJTA",src="FRED")
getSymbols("DJUA",src="FRED")   DJ <- merge(DJIA,DJTA,DJUA)   #DJ.yearly <- DJ[endpoints(DJ, on="years", k=1),]
DJ.roc <- ROC(DJ,n=1,type="discrete")     #another method of viewing drawdowns
#this is really easy with PerformanceAnalytics
#here is how to apply the very nice example
#provided in the documentation   DJ.draw = Drawdowns(DJ.roc[,1])
drawdowns = table.Drawdowns(DJ.roc[,1])                          
#jpeg(filename="DJIA worst drawdown event chart.jpg",
# quality=100,width=6.25, height = 6.25,  units="in",res=96)
chart.Events(DJ.draw,
 dates = drawdowns$Trough, prior=max(na.omit(drawdowns$"To Trough")),
 post=max(na.omit(drawdowns$Recovery)),
 lwd=2, colorset=redfocus, legend.loc=NULL,
 main = "DJIA Worst Drawdowns")
#dev.off()
#drawdown is so long in 1929 that it messes up the chart
#let's limit this to two years or 750 trading days
#jpeg(filename="DJIA worst drawdown event chart with limit.jpg",
# quality=100,width=6.25, height = 6.25,  units="in",res=96)
chart.Events(DJ.draw,
 dates = drawdowns$Trough, prior=max(na.omit(drawdowns$"To Trough")),
 post=min(750,max(na.omit(drawdowns$Recovery))),
 lwd=2, colorset=redfocus, legend.loc=NULL,
 main = "DJIA Worst Drawdowns
 with Recovery Limit at 750 Days")
#dev.off()   #now let's do it for GDP
getSymbols("GDP",src="FRED")
GDP.roc <- ROC(GDP,type="discrete",n=1)
GDP.draw = Drawdowns(GDP.roc[,1])
drawdownsGDP = table.Drawdowns(GDP.roc[,1])                          
#jpeg(filename="GDP worst drawdown event chart.jpg",
# quality=100,width=6.25, height = 6.25,  units="in",res=96)
chart.Events(GDP.draw,
 dates = drawdownsGDP$Trough, prior=max(na.omit(drawdownsGDP$"To Trough")),
 post=max(na.omit(drawdownsGDP$Recovery)),
 lwd=2, colorset=redfocus, legend.loc="bottomright",xlab="Quarters +/- Drawdown",
 main = "US GDP Worst Drawdowns")
#dev.off()
```

由 Pretty R 在 inside-R.org 创建](http://www.inside-r.org/pretty-r "由 Pretty R 在 inside-R.org 创建")
