<!--yml

类别：未分类

日期: 2024-05-18 15:11:31

-->

# Timely Portfolio：我最好的想法之一在一个困难的月份

> 来源：[`timelyportfolio.blogspot.com/2011/09/difficult-month-for-one-of-my-best.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/09/difficult-month-for-one-of-my-best.html#0001-01-01)

THIS IS NOT INVESTMENT ADVICE.  MY IDEAS PROBABLY WILL LOSE YOU MONEY, AND I WILL NOT LET YOU KNOW WHEN I CHANGE MY MIND.

彭博社的文章“[亚洲货币预计创下自 1997 年危机以来最差表现，引发了国际货币基金组织的紧急援助](http://www.bloomberg.com/news/2011-09-30/asia-currencies-set-for-worst-month-since-97.html)”说明了为什么在我所有的看空情绪中，我这个月没赚到多少钱。作为对不太忠实读者的提醒，[`timelyportfolio.blogspot.com/2011/05/russell-napier-asip-in-ft-says-emerging.html`](http://timelyportfolio.blogspot.com/2011/05/russell-napier-asip-in-ft-says-emerging.html "http://timelyportfolio.blogspot.com/2011/05/russell-napier-asip-in-ft-says-emerging.html")显示了我为什么喜欢做多新兴市场股票和做空 Russell 2000。然而，当货币受到重创时，这种交易效果并不好。我理解 1997 年当索罗斯等人控制着亚洲货币时，它们受到重创，但是 15 年 10 万亿美元自那次危机以来，亚洲央行显然已经控制了自己的货币，如果他们选择施加影响的话。相对于外币（参见帖子[加入储备](http://timelyportfolio.blogspot.com/2011/07/join-reserves.html)）主要是美元，数十亿美元的外流无关紧要。

R 代码：

require(quantmod)

#从美国联邦储备银行数据系列获取亚洲货币数据

getSymbols("DEXKOUS",src="FRED") #加载韩国

getSymbols("DEXMAUS",src="FRED") #加载马来西亚

getSymbols("DEXSIUS",src="FRED") #加载新加坡

getSymbols("DEXTAUS",src="FRED") #加载台湾

getSymbols("DEXCHUS",src="FRED") #加载中国

getSymbols("DEXJPUS",src="FRED") #加载日本

getSymbols("DEXTHUS",src="FRED") #加载泰国

getSymbols("DEXBZUS",src="FRED") #加载巴西

getSymbols("DEXMXUS",src="FRED") #加载墨西哥

getSymbols("DEXINUS",src="FRED") #加载印度

getSymbols("DTWEXO",src="FRED") #加载美元其他贸易伙伴

getSymbols("DTWEXB",src="FRED") #加载美元广泛

par(mfrow=c(4, 3)) #为图表提供 2 列和 3 行

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

绘制(coredata(DTWEXO["1995::2011"]),类型="l",y 轴标签="其他美元")

绘制(coredata(DTWEXB["1995::2011"]),类型="l",y 轴标签="宽泛美元")
