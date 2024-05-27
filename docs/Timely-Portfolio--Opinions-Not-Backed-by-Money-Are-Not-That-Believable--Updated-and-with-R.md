<!--yml

分类：未分类

日期：2024-05-18 15:22:20

-->

# 及时投资组合：没有金钱支持的观点并不可信——更新版及 R 语言版

> 来源：[`timelyportfolio.blogspot.com/2011/02/opinions-not-backed-by-money-are-not.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/02/opinions-not-backed-by-money-are-not.html#0001-01-01)

作为对[`timelyportfolio.blogspot.com/2010/12/opinions-not-backed-with-money-are-not.html`](http://timelyportfolio.blogspot.com/2010/12/opinions-not-backed-with-money-are-not.html "http://timelyportfolio.blogspot.com/2010/12/opinions-not-backed-with-money-are-not.html")的更新，我更新了修订数据，加入了过去两个月的内容，并翻译成了 R。

如果世界真的像一些人所说的那样过于乐观地看待股市，我想钱会明显地流向那个方向。[雷文·布伦纳](http://www.google.com/url?sa=t&source=web&cd=2&sqi=2&ved=0CCkQFjAB&url=http%3A%2F%2Fpeople.mcgill.ca%2Freuven.brenner%2F&ei=AtoDTdCzPIL68AaHkN3oAg&usg=AFQjCNEuEABpeGQTvMWHn65c3m2UEiNx7A&sig2=72tzgAtmCJeMjFpdsSwQWg "雷文·布伦纳")在《赌博与投机》（[Gambling and Speculation](http://www.amazon.com/Gambling-Speculation-Theory-History-Decisions/dp/0521381800/ref=sr_1_6?ie=UTF8&qid=1292098820&sr=8-6 "http://www.amazon.com/Gambling-Speculation-Theory-History-Decisions/dp/0521381800/ref=sr_1_6?ie=UTF8&qid=1292098820&sr=8-6")）一书中为追求财富改善的赌博或冒险行为提供了一些理由：娱乐、过度自信、在概率评估能力较强的情况下采取的理性行动，以及绝望或相对表现不佳。

娱乐在投资中可以被排除，因为娱乐主要在赌注较低的情况下占主导地位。

然而，促使冒险的另外三个原因在当前看似强烈的看涨环境中都非常容易适用。然而，分析一个我没有在媒体中看到的图表，揭示了一个有趣的结果。根据[ICI](http://www.google.com/url?sa=t&source=web&cd=1&ved=0CBoQFjAA&url=http%3A%2F%2Fwww.ici.org%2F&ei=6eADTa-EGYOBlAfowcmuDg&usg=AFQjCNHp-bkB5qtA4VrXR6oCgdo_7jq_Tw&sig2=Mb8QzLDFXlWir56i5jOCkA "ICI")的数据显示，由于 2007-2008 年的金融危机，股票 mutual fund 出现了大量外流，而这种外流一直持续到 2009 年 3 月以来的所谓“泡沫牛市”期间，这是由危机的严重性引起的持续恐惧所驱动的。当我们把 2009 年至今的时期与最近的 1987 年(ICI 系列的开始)-2000 年和 2003-2007 年的牛市相比较时，股票 mutual fund 的流动明显不同，并且没有显示出与经常引用的[AAII- The American Association of Individual Investors](http://www.google.com/url?sa=t&source=web&cd=1&sqi=2&ved=0CBsQFjAA&url=http%3A%2F%2Faaii.com%2F&ei=BOIDTZq_H8OB8gbe36TrAg&usg=AFQjCNH43QiLqrZG9YBv_pvV1H-0qBeJoQ&sig2=Vdg0bSGYfr3vuS7SyBVw5w "AAII- The American Association of Individual Investors")情绪调查之间的实际相关性。该调查显示了不同程度的看涨和看跌情绪，但观点并没有影响到股票 mutual fund 的流出。无论看涨情绪是由过度自信还是对概率的理性评估所 justified，它都没有足够的力量来说服投资者追求改善财富的潜在机会。

如果这种由于原因 2 和 3 结合以及原因 4 的绝望而导致的看涨情绪还没有驱使资金流向机会，那么恐惧主导着一切。如果恐惧主导，那么机会将被浪费，而美国日益增加的、但已经创纪录的收入/财富不平等以及每个人储蓄的戏剧性表现不佳（过度投资于债券）将引发更多的绝望。最终，如果出于某种原因 2 和 3 没有首先发挥作用，这种绝望将变得如此严重，以至于它将迫使投资者承担风险。其确切表现尚不清楚，但它将出现在债券之外的地方。过度自信和绝望的风险承担会导致泡沫，由于我们还没有看到任何真正的风险承担，所以目前股票市场上不存在泡沫。

来自[AAII- The American Association of Individual Investors](http://www.google.com/url?sa=t&source=web&cd=1&sqi=2&ved=0CBsQFjAA&url=http%3A%2F%2Faaii.com%2F&ei=BOIDTZq_H8OB8gbe36TrAg&usg=AFQjCNH43QiLqrZG9YBv_pvV1H-0qBeJoQ&sig2=Vdg0bSGYfr3vuS7SyBVw5w "AAII- The American Association of Individual Investors")和[ICI](http://www.google.com/url?sa=t&source=web&cd=1&ved=0CBoQFjAA&url=http%3A%2F%2Fwww.ici.org%2F&ei=6eADTa-EGYOBlAfowcmuDg&usg=AFQjCNHp-bkB5qtA4VrXR6oCgdo_7jq_Tw&sig2=Mb8QzLDFXlWir56i5jOCkA "ICI")的数据表明：

[`spreadsheets.google.com/ccc?key=0Amqp2r96khJPdENIRnE1SG5nanJ5OXFyYVUxOXRBVmc&hl=en`](https://spreadsheets.google.com/ccc?key=0Amqp2r96khJPdENIRnE1SG5nanJ5OXFyYVUxOXRBVmc&hl=en "https://spreadsheets.google.com/ccc?key=0Amqp2r96khJPdENIRnE1SG5nanJ5OXFyYVUxOXRBVmc&hl=en")

For the R geeks:

require(quantmod)

require(ggplot2)

aaii_ici=read.csv("aaii-ici-noblank.csv",row.names=1)

#using ggplot example from [`learnr.wordpress.com/2009/03/16/ggplot2-split-data-range-into-multiple-chart-series/`](http://learnr.wordpress.com/2009/03/16/ggplot2-split-data-range-into-multiple-chart-series/)

p <- ggplot(data=aaii_ici, aes(x = AAIIBULL-AAIIBEAR, y = runSum(aaii_ici[,4],3), colour = Range, shape = Range, label = Range))

p1 <- p + geom_point() + scale_y_continuous(limits = c(-200000, 200000),formatter=comma) + geom_hline(yintercept=0) + geom_vline(xintercept=0) + stat_smooth(method="lm", se=FALSE) + ylab("ICI Equity Rolling 3-mo Sum") + opts(title = "ICI Equity Flows by AAII Survey")

print(p1)
