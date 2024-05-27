<!--yml

category: 未分类

date: 2024-05-18 15:08:01

-->

# Timely Portfolio: 再次更新并不以金钱为后盾的观点

> 来源：[`timelyportfolio.blogspot.com/2012/03/opinions-not-backed-by-money-updated.html#0001-01-01`](http://timelyportfolio.blogspot.com/2012/03/opinions-not-backed-by-money-updated.html#0001-01-01)

很奇怪我正在第三次更新这篇文章，但实际上没有什么改变，但没有改变的事实对我来说非常有趣。由于这是一次更新，我不会重复解释，请阅读上一个版本[不以金钱为后盾的观点并不那么可信--更新并使用 R](http://timelyportfolio.blogspot.com/2011/02/opinions-not-backed-by-money-are-not.html)。基本结论是我们处于牛市，AAII 调查持多头看好，但没有人愿意在股市上打好注。

数据在 Google 文档中（[`docs.google.com/spreadsheet/ccc?key=0Amqp2r96khJPdENIRnE1SG5nanJ5OXFyYVUxOXRBVmc`](https://docs.google.com/spreadsheet/ccc?key=0Amqp2r96khJPdENIRnE1SG5nanJ5OXFyYVUxOXRBVmc "https://docs.google.com/spreadsheet/ccc?key=0Amqp2r96khJPdENIRnE1SG5nanJ5OXFyYVUxOXRBVmc")）来源自[AAII- 美国个体投资者协会](http://www.google.com/url?sa=t&source=web&cd=1&sqi=2&ved=0CBsQFjAA&url=http%3A%2F%2Faaii.com%2F&ei=BOIDTZq_H8OB8gbe36TrAg&usg=AFQjCNH43QiLqrZG9YBv_pvV1H-0qBeJoQ&sig2=Vdg0bSGYfr3vuS7SyBVw5w) 和 [ICI](http://www.google.com/url?sa=t&source=web&cd=1&ved=0CBoQFjAA&url=http%3A%2F%2Fwww.ici.org%2F&ei=6eADTa-EGYOBlAfowcmuDg&usg=AFQjCNHp-bkB5qtA4VrXR6oCgdo_7jq_Tw&sig2=Mb8QzLDFXlWir56i5jOCkA)。

R 代码（甚至不值得放在 GIST 中）：

require(quantmod)

require(ggplot2)

aaii_ici=read.csv("aaii-ici-noblank.csv",row.names=1)

#使用 ggplot 示例来自 [`learnr.wordpress.com/2009/03/16/ggplot2-split-data-range-into-multiple-chart-series/`](http://learnr.wordpress.com/2009/03/16/ggplot2-split-data-range-into-multiple-chart-series/)

p <- ggplot(data=aaii_ici, aes(x = AAIIBULL-AAIIBEAR, y = runSum(aaii_ici[,4],3), colour = Range, shape = Range, label = Range))

p1 <- p + geom_point() + scale_y_continuous(limits = c(-200000, 200000),formatter=comma) + geom_hline(yintercept=0) + geom_vline(xintercept=0) + stat_smooth(method="lm", se=FALSE) + ylab("ICI Equity Rolling 3-mo Sum") + opts(title = "AAII 调查的 ICI 股票滚动 3 个月总和")

print(p1)
