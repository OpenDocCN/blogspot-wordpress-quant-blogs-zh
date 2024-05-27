<!--yml

类别：未分类

日期：2024-05-18 15:12:17

-->

# Timely Portfolio: Real Squeeze

> 来源：[`timelyportfolio.blogspot.com/2011/08/real-squeeze.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/08/real-squeeze.html#0001-01-01)

实际收益率现在已经被完全压缩到 10 年。要么债券投资者需要接受更糟糕的实际负收益率，要么通货紧缩需要变得丑陋，从这里获得额外的价格回报。如果通货紧缩是结果，那么与长期债券相比，做空股票和商品将更有回报。

代码：

需要(quantmod)

获取符号("DGS10",来源="FRED")

获取符号("DFII10",来源="FRED")

条形图(rbind(合并(DGS10["2010-12-31",]-DFII10["2010-12-31",],DFII10["2010-12-31",]),

合并(DGS10[NROW(DGS10),]-DFII10[NROW(DFII10),],DFII10[NROW(DFII10),])),

颜色=c("steelblue3","firebrick3"),

主标题="美国 10 年收益率组成部分

YTD 2011 变更",

y 限制=c(0,4))

文本(y=c(coredata(DGS10["2010-12-31",])-.3,coredata(DFII10["2010-12-31",]),

coredata(DGS10[NROW(DGS10),])-.02,coredata(DFII10["2010-12-31",])),

x=c(0.7,0.7,1.9,1.9),

c(粘贴("real",sprintf("%.2f",coredata(DFII10["2010-12-31",])),sep=" "),

粘贴("inflation",sprintf("%.2f",coredata(DGS10["2010-12-31",]-DFII10["2010-12-31",])),sep=" "),

粘贴("real",sprintf("%.2f",coredata(DFII10[NROW(DFII10),])),sep=" "),

粘贴("inflation",sprintf("%.2f",coredata(DGS10[NROW(DGS10),]-DFII10[NROW(DFII10),])),sep=" ")),

字体大小=0.8)
