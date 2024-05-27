<!--yml

category: 未分类

date: 2024-05-18 15:22:56

-->

# 及时的投资组合：日本是故意的还是意外的追求通货紧缩

> 来源：[`timelyportfolio.blogspot.com/2011/02/japan-intentional-or-accidental-pursuit.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/02/japan-intentional-or-accidental-pursuit.html#0001-01-01)

日本故意或意外地追求通货紧缩造成的不平衡比伯南克追求通货膨胀更为严重。日本政策制定者已经允许日元对所有其他货币升值。他们似乎认识到了几个问题：

> 1）较高的利率和通货膨胀对他们的信用风险、赤字资金和老龄化人口构成了比通货紧缩更大的风险。
> 
> 2）发达市场被日本商品充斥，进一步的日元升值不会瘫痪这些出口。

但是，通过认识到这两个问题，他们正在允许新兴市场的竞争和潜在增长动力完全利用它们。韩国的现代和三星在价格上比其日本竞争对手具有 30-50%的优势。

日本试图避免因高利率和通货膨胀而不可避免地崩溃，加速了由新兴市场竞争引起的崩溃。市场最终将强加对日本情况的调整。至少伯南克认识到了由亚洲货币低估引起的不平衡，并知道通货膨胀是唯一的机制，可以迫使亚洲新兴国家允许其货币升值到正常估值，即使这最终意味着对美国的艰难决策。

较低的利率鼓励不平衡，而较高的利率迫使必要的变化以纠正这些不平衡。

自 1997 年亚洲崩溃的最低点以来，日本是否比新兴亚洲国家更好？

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjzt0po1UovpXVipfSBHgGcAFXBwbnnBaw1usaLEXRTMEyIlLKI0hQcf_962K6QUCQcMVYn4urSMsS_xJ0AhV5_dBG3_9pH8nPZI8FLBtQjYbniY42pVdnXJRtH0Q5UL3hNDk1looHeLg/s1600-h/image%5B22%5D.png)

自 2007 年以来，日本是否比新兴亚洲国家更好？

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg_zemtkWwQ0FXrEzwsRVIw_uUv3zVv-SvxSza9PMY6lzl0wy30lMVc7p-6aMsakOZ_nYzRfcZQrG1upAU8-R5JRyxl3bUhoKo-7B23Id7HD9myxYwxQf5RSBXMpw4-GAGs2N3Ed-km0Q/s1600-h/image%5B25%5D.png)

作为参考，这里是[OECD 对韩国与日本购买力平价的计算](http://www.oecd.org/document/47/0,3746,en_2649_34357_36202863_1_1_1_1,00.html)184，这意味着韩元对日元的汇率被低估了 84%。[《经济学人》的巨无霸指数](http://www.economist.com/markets/Bigmac/index.cfm)显示亚洲货币对日元的低估幅度为 40-50%。

日本的决定在股票市场中受到了不友好的对待

![]![](http://stockcharts.com/h-sc/ui?s=%24p3dow:%24nikk&p=w&yr=12&mn=6&dy=0&id=p81676149069)

通过[StockCharts.com](http://stockcharts.com/h-sc/ui?s=%24p3dow:%24nikk&p=w&yr=12&mn=6&dy=0&id=p81676149069)

对于这里的编程爱好者，这是代码：

需要(quantmod)

需要(PerformanceAnalytics)

从美联储 FRED 数据系列中获取亚洲货币数据

getSymbols("DEXKOUS",src="FRED") #load Korea

getSymbols("DEXMAUS",src="FRED") #load Malaysia

getSymbols("DEXSIUS",src="FRED") #load Singapore

getSymbols("DEXTAUS",src="FRED") #load Taiwan

getSymbols("DEXCHUS",src="FRED") #load China

getSymbols("DEXJPUS",src="FRED") #load Japan

asian<-merge(DEXKOUS,DEXMAUS,DEXSIUS,DEXTAUS,DEXCHUS,DEXJPUS)

进行 dailyReturn，这样我就可以使用漂亮的 PerformanceAnalytics 图表

除法将货币转换为日元，从美元开始

asianreturn<-merge(dailyReturn(asian[,6]/asian[,1],subset="1996::"),dailyReturn(asian[,6]/asian[,2],subset="1996::"),dailyReturn(asian[,6]/asian[,3],subset="1996::"),dailyReturn(asian[,6]/asian[,4],subset="1996::"),dailyReturn(asian[,6]/asian[,5],subset="1996::"))

#为图表 legends 标记列

colnames(asianreturn)<-c("Korea","Malaysia","Singapore","Taiwan","China")

chart.CumReturns(asianreturn,ylim=c(-0.4,0.4),legend.loc="topright",main="亚洲货币对日元",ylab="",period.areas=list(c("Sep 97","Dec 97"),c("Jun 04","Nov 06"),c("Dec 07","Mar 09")),period.color="gray",event.lines=c("Dec 97","Nov 06","Mar 09"),event.labels=c("亚洲虎崩溃","套利交易","金融危机"),event.color="black")

mtext("Source: Federal Reserve FRED",side=1,adj=0)

chart.Drawdown(asianreturn['2006-11-30::',],legend.loc="right",main="亚洲货币对日元",ylab="金融危机以来的回撤")

mtext("Source: Federal Reserve FRED",side=1,adj=0)

*3.5 小时*
