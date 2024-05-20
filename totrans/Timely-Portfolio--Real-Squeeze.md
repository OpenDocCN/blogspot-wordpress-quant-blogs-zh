<!--yml
category: 未分类
date: 2024-05-18 15:12:17
-->

# Timely Portfolio: Real Squeeze

> 来源：[http://timelyportfolio.blogspot.com/2011/08/real-squeeze.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/08/real-squeeze.html#0001-01-01)

Real yields even out to 10 years have now been competely squeezed. Either bond investors need to accept even worse negative real yields or deflation needs to get ugly for additional price returns from here. If deflation is the outcome, then shorts in stocks and commodities will be much more rewarding than long bonds.

R code:

require(quantmod)

getSymbols("DGS10",src="FRED")
getSymbols("DFII10",src="FRED")

barplot(rbind(merge(DGS10["2010-12-31",]-DFII10["2010-12-31",],DFII10["2010-12-31",]),
    merge(DGS10[NROW(DGS10),]-DFII10[NROW(DFII10),],DFII10[NROW(DFII10),])),
    col=c("steelblue3","firebrick3"),
    main="US 10 Year Yield Components
    YTD 2011 Change",
    ylim=c(0,4))
text(y=c(coredata(DGS10["2010-12-31",])-.3,coredata(DFII10["2010-12-31",]),
    coredata(DGS10[NROW(DGS10),])-.02,coredata(DFII10["2010-12-31",])),
    x=c(0.7,0.7,1.9,1.9),
    c(paste("real",sprintf("%.2f",coredata(DFII10["2010-12-31",])),sep=" "),
    paste("inflation",sprintf("%.2f",coredata(DGS10["2010-12-31",]-DFII10["2010-12-31",])),sep=" "),
    paste("real",sprintf("%.2f",coredata(DFII10[NROW(DFII10),])),sep=" "),
    paste("inflation",sprintf("%.2f",coredata(DGS10[NROW(DGS10),]-DFII10[NROW(DFII10),])),sep=" ")),
    cex=0.8)