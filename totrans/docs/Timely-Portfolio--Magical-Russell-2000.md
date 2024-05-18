<!--yml
category: 未分类
date: 2024-05-18 15:10:46
-->

# Timely Portfolio: Magical Russell 2000

> 来源：[http://timelyportfolio.blogspot.com/2011/11/i-have-marveled-at-magical-russell-2000.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/11/i-have-marveled-at-magical-russell-2000.html#0001-01-01)

I have marveled at the magical Russell 2000 in [Crazy RUT](http://timelyportfolio.blogspot.com/2011/07/crazy-rut.html), but I am still surprised at its behavior through this selloff.  With a 20-day move of 30% (6% in one hour) and big outperformance to the developed and developing world, the Russell 2000 continues its magical display.

R code:

#look at distance from the 3 month minimum
#to compare the magical US Russell 2000
#to the world

require(quantmod)

tkrs <- c("^W2DOW","^RUT")

getSymbols(tkrs,from="1896-01-01",to=Sys.Date())

#merge the closing values
markets <- na.omit(merge(W2DOW[,4],RUT[,4]))

#this is ugly but it works
altitude <- function(x) x/min(x)-1
mins <- as.xts(apply(markets[(NROW(markets)-250):NROW(markets),1:2],
    MARGIN=2,FUN=
    altitude))
plot.zoo(mins,screens=1,
    col=c("cadetblue4","darkolivegreen3"),
    lwd=2,ylab="% from 250 day minimum",xlab=NA,
    main="Russell 2000 and DJ World ex US
    Distance from 250 Day Minimum")
legend("bottom",c("DJ World ex US","Russell 2000"),lty=1,lwd=2,
    col=c("cadetblue4","darkolivegreen3"),horiz=TRUE)