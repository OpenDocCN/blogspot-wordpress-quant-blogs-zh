<!--yml

category: 未分类

date: 2024-05-18 14:58:04

-->

# Timely Portfolio: Stocks and Bonds Behavior by Decade

> 来源：[`timelyportfolio.blogspot.com/2013/08/stocks-and-bonds-behavior-by-decade.html#0001-01-01`](http://timelyportfolio.blogspot.com/2013/08/stocks-and-bonds-behavior-by-decade.html#0001-01-01)

I struggled with whether or not I should even post this.  It is raw and ugly, but it might help somebody out there.   I might use this as a basis for some more gridSVG posts, but I do not think I have the motivation to finish the analysis.

![ggplot stocks bonds by decade](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjrCsCFbFk6Zjet8fvsyr3CNxBtzhKJyys5mNjSiQGtmyYXNmU3wnOoqjIUStmZBhLh-izt3bK00u1eUcEp4xu0YS2UXF0AKNOd3Bs_8uJQGeiMEbrp6AF5g2V-2-yH-AbF3VxDzm1hAg/s1600-h/ggplot%252520stocks%252520bonds%252520by%252520decade%25255B1%25255D.jpg)![performance by time](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg9gHHO1I1AGxFyCQrvLHu5rB-npQdAXdpe3xEQq8Tycgq-QlAftguhN4LVrXg6LWU4B6RuGusqqbvxtRFcgP_xIWkgmLjCTm5bi3RK2tPKHXLdy6kBpfnLEC4laM4s4KZZLgWF7tuuRw/s1600-h/performance%252520by%252520time%25255B1%25255D.jpg)![lattice stocks bonds by decade](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjY6Rl5cXmXgJgw_79t1iyXEFaqBOkSAt2S4cT4-GIwc465L1w-XoY9ZrKFKEbcGfdWotQ06NH9O80YarIQdIwcSa4K6z4la0UJKcEHQ0930VAt9DfTSw5tVU9_ikSTKeiBlpkeoRI3VA/s1600-h/lattice%252520stocks%252520bonds%252520by%252520decade%25255B1%25255D.jpg)![perf summar](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi1Ych6jFeXNO_IVC6p1p0wK34ILPlIneKh2rYvcMq7f7meGS38fBlKrU5so92d4_qF-U_qMuGlZZ3xvLG0SA7idMTkkaWuqskdWhx-9oPa3Ns-V8iyHc8nYzBVrEa926nquw881MMTEw/s1600-h/perf%252520summar%25255B1%25255D.jpg)

Code:

require(latticeExtra)

require(quantmod)

require(PerformanceAnalytics)

getSymbols("SP500",src="FRED")

US10 <- na.omit(getSymbols("DGS10",src="FRED",auto.assign=FALSE))

stocksBonds <- na.omit(

merge(

lag(SP500,k=-100)/SP500-1,  #forward 100 day sp500 perf

US10 / runMean(US10,n=250) - 1,       #us10 yield - 250 day average

SP500

)

)

#get the decade

stocksBonds$decade = as.numeric(substr(index(stocksBonds),1,3)) * 10

#name columns

colnames(stocksBonds) <- c("sp500","us10","SP500","decade")

#get a color ramp for our change in us10 year yields

linecolors <- colorRamp(

c("红色","绿色"),

interpolate="linear",

space="rgb"

)((stocksBonds[,2]+0.5))

xyplot(

stocksBonds[,1],

col=rgb(linecolors,max=255),

type="p",pch=19,cex=0.5,

main = "Stocks 100d Forward Performance"

)

xyplot(

sp500 ~ us10 | factor(decade),

groups = decade,

data = as.data.frame(stocksBonds),

pch=19,

cex = 0.5,

scales = list(

x = list(tck=c(1,0),alternating=1)

),

layout=c(6,1),

`main = "S&P 500 Forward Performance vs US 10y Change in Yields",`

`ylab = "S&P Forward Performance (100d)",`

`xlab = "US 10y Yields - 250d Avg"`

`) +`

`latticeExtra::layer(panel.abline(h=0,col="gray",lty=2)) +`

`latticeExtra::layer(panel.abline(v=0,col="gray",lty=2)) +`

`xyplot(`

`sp500 ~ us10 | factor(decade),`

`col="gray",`

`data = as.data.frame(stocksBonds),`

`panel = panel.lmline)`

`require(ggplot2)`

`ggplot(data = data.frame(stocksBonds), aes(y=sp500, x= us10,colour=decade))+`

`geom_point()+facet_wrap(~decade,ncol=6)+geom_smooth()`

`charts.PerformanceSummary(`

`merge(`

`ROC(stocksBonds[,3],n=1,type="discrete"),`

`ROC(stocksBonds[,3],n=1,type="discrete") * (stocksBonds[,2]>0)`

`),`

`main="S&P 500 | if Bonds - Mean(250d) > 0"`

`)`
