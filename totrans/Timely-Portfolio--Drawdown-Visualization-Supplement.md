<!--yml
category: 未分类
date: 2024-05-18 15:12:09
-->

# Timely Portfolio: Drawdown Visualization Supplement

> 来源：[http://timelyportfolio.blogspot.com/2011/08/drawdown-visualization-supplement.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/08/drawdown-visualization-supplement.html#0001-01-01)

As commented on [Drawdown Visualization](http://timelyportfolio.blogspot.com/2011/08/drawdown-visualization.html),

> “Also, take a look at the example in ?chart.Event for another visualization of drawdowns, in this case stacking them for comparison.”

the PerformanceAnalytics package offers a very helpful look at the path of drawdowns that we can apply to financial and economic time series.  Here is the result applied to the Dow Jones Industrial Average since 1896.

1929-1954 really messes this chart up, so let's limit the recovery to 750 days to get a better visualization.

I thought it would be even more fun to apply this example to the GDP series.  This could be extended to all sorts of interesting economic data—first in my mind are industrial production and consumer spending.

R code (click to download from Google Docs):

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

[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")