<!--yml

category: 未分类

date: 2024-05-18 15:10:46

-->

# 及时投资组合：神奇的罗素 2000

> 来源：[`timelyportfolio.blogspot.com/2011/11/i-have-marveled-at-magical-russell-2000.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/11/i-have-marveled-at-magical-russell-2000.html#0001-01-01)

I 在[疯狂 RUT](http://timelyportfolio.blogspot.com/2011/07/crazy-rut.html)中惊叹于神奇的罗素 2000，但我仍然对它在这次抛售中的表现感到惊讶。在一个 20 天的 30%的移动（在一个小时内 6%）以及相对于发达和发展中世界的巨大超额表现下，罗素 2000 继续展示着它的魔法。

R 代码：

#查看从 3 个月最低点的距离

#比较神奇的美国罗素 2000

#到世界各地

require(quantmod)

tkrs <- c("^W2DOW","^RUT")

getSymbols(tkrs,from="1896-01-01",to=Sys.Date())

#合并收盘价

markets <- na.omit(merge(W2DOW[,4],RUT[,4]))

#这很丑，但管用

altitude <- function(x) x/min(x)-1

mins <- as.xts(apply(markets[(NROW(markets)-250):NROW(markets),1:2],

MARGIN=2,FUN=

altitude))

plot.zoo(mins,screens=1,

col=c("cadetblue4","darkolivegreen3"),

lwd=2,ylab="% from 250 day minimum",xlab=NA,

main="罗素 2000 和道琼斯世界除美国

距 250 天最低点的距离")

legend("bottom",c("道琼斯世界除美国","罗素 2000"),lty=1,lwd=2,

col=c("cadetblue4","darkolivegreen3"),horiz=TRUE)
