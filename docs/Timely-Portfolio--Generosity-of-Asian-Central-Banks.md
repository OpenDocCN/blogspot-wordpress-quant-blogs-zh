<!--yml

类别：未分类

日期：2024-05-18 15:11:19

-->

# 及时投资组合：亚洲中央银行的慷慨

> 来源：[`timelyportfolio.blogspot.com/2011/10/generosity-of-asian-central-banks.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/10/generosity-of-asian-central-banks.html#0001-01-01)

唯一区分美国与欧洲以及臭名昭著的 PIIGS 的是亚洲中央银行的慷慨，自 1998 年以来它们一直在持续量化宽松([加入储备](http://timelyportfolio.blogspot.com/2011/07/join-reserves.html))。

如果没有这种慷慨，美国很可能会在 2008 年进入死亡螺旋（参见[一个国家的死亡螺旋](http://timelyportfolio.blogspot.com/2011/03/death-spiral-of-country.html)和[死亡螺旋警告图表](http://timelyportfolio.blogspot.com/2011/03/death-spiral-warning-graph.html)），并且仍然可能掉入这个灾难性的陷阱。

故意攻击这条非常脆弱的线索似乎是愚蠢的，但这种愚蠢的行为得到了我们优秀政治家的支持[华盛顿邮报“参议院批准中国货币法案”](http://www.washingtonpost.com/blogs/2chambers/post/senate-approves-china-currency-bill/2011/10/11/gIQAhvaUdL_blog.html)。美国需要招募一些美元买家，但不幸的是，没有填补万亿美元空缺的买家。

更令人担忧的是，人们将焦点放在中国，而中国一直在稳步解决问题。当你看到人民币的升值时，将焦点放在中国是没有意义的。我在路上看到了很多韩国汽车，商店里有电视和家电，但我没有听到任何人提到韩元对美元的极端低估，特别是对日元的低估，所以看起来韩元被低估了。

我同意美国$储备的增加需要停止，但请不要故意引发一个正反馈死亡螺旋。

[R 代码（点击从谷歌文档下载）：](https://docs.google.com/leaf?id=0B2qp2r96khJPMDVjMWE3ZjktMTM0Yi00MzkyLWI0MmQtOWM5MTBjNzRmYzBh&hl=en_US)

require(quantmod)

require(PerformanceAnalytics)

getSymbols("DEXCHUS",src="FRED")

getSymbols("DEXKOUS",src="FRED")

plot.zoo(merge(1/DEXCHUS,100/DEXKOUS)["1997::",],screens=1,lwd=2,

col=c("lightblue4","antiquewhite4"),

xlab="Year",ylab=NA,

main="中国人民币和韩国元

1997 年至 2011 年 9 月")

legend("right", c("中国","韩国"), lwd = 2, bty="n",

col=c("lightblue4","antiquewhite4"),y.intersp=2,

text.col=c("lightblue4","antiquewhite4"))
