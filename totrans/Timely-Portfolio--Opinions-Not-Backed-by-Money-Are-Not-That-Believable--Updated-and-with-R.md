<!--yml
category: 未分类
date: 2024-05-18 15:22:20
-->

# Timely Portfolio: Opinions Not Backed by Money Are Not That Believable--Updated and with R

> 来源：[http://timelyportfolio.blogspot.com/2011/02/opinions-not-backed-by-money-are-not.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/02/opinions-not-backed-by-money-are-not.html#0001-01-01)

As an update to [http://timelyportfolio.blogspot.com/2010/12/opinions-not-backed-with-money-are-not.html](http://timelyportfolio.blogspot.com/2010/12/opinions-not-backed-with-money-are-not.html "http://timelyportfolio.blogspot.com/2010/12/opinions-not-backed-with-money-are-not.html"), I have updated the revised data, added the past two months, and translated to R.

If the world really is overly bullish on stocks as some suggest, I would think money would flow visibly in that direction.  [Reuven Brenner](http://www.google.com/url?sa=t&source=web&cd=2&sqi=2&ved=0CCkQFjAB&url=http%3A%2F%2Fpeople.mcgill.ca%2Freuven.brenner%2F&ei=AtoDTdCzPIL68AaHkN3oAg&usg=AFQjCNEuEABpeGQTvMWHn65c3m2UEiNx7A&sig2=72tzgAtmCJeMjFpdsSwQWg "Reuven Brenner") in [Gambling and Speculation](http://www.amazon.com/Gambling-Speculation-Theory-History-Decisions/dp/0521381800/ref=sr_1_6?ie=UTF8&qid=1292098820&sr=8-6 "http://www.amazon.com/Gambling-Speculation-Theory-History-Decisions/dp/0521381800/ref=sr_1_6?ie=UTF8&qid=1292098820&sr=8-6") offers some reasons for gambling or risk-taking in pursuit of wealth improvement:  entertainment,  overconfidence, rational action given competent assessment of probability, and desperation or relative underperformance.

Entertainment can be eliminated in the case of investing, since entertainment prevails primarily when the stakes are low.

The other three reasons for risk-taking however would in the current environment of supposedly strong bullishness all very readily apply.  However, analysis of a chart that I have surprisingly not seen in the press, reveals an interesting result.  Mutual fund flows as measured by [ICI](http://www.google.com/url?sa=t&source=web&cd=1&ved=0CBoQFjAA&url=http%3A%2F%2Fwww.ici.org%2F&ei=6eADTa-EGYOBlAfowcmuDg&usg=AFQjCNHp-bkB5qtA4VrXR6oCgdo_7jq_Tw&sig2=Mb8QzLDFXlWir56i5jOCkA "ICI") show an exodus from equities precipitated by the financial panic of 2007-2008 but extended throughout the supposedly “bubble bull market” since March 2009 driven by lingering effects of fear due to the severity of the crisis.  When we compare the 2009-current period to the most recent bull markets of 1987 (start of the ICI series)-2000 and 2003-2007, equity mutual fund flows are markedly different and do not exhibit any real correlation to the often cited sentiment survey of the [AAII- The American Association of Individual Investors](http://www.google.com/url?sa=t&source=web&cd=1&sqi=2&ved=0CBsQFjAA&url=http%3A%2F%2Faaii.com%2F&ei=BOIDTZq_H8OB8gbe36TrAg&usg=AFQjCNH43QiLqrZG9YBv_pvV1H-0qBeJoQ&sig2=Vdg0bSGYfr3vuS7SyBVw5w "AAII- The American Association of Individual Investors").  The survey displays varying degrees of bullishness and bearishness, but opinion has not affected the outflow from equity mutual funds.  Whether the bullishness is justified by overconfidence or rational assessment of probability, it has not been strong enough to convince investors to pursue a potential opportunity to improve wealth.

If this bullishness through reasons 2 and 3 combined with the fourth reason of desperation has not driven money to opportunity, then fear dominates. If fear dominates, then opportunity will be squandered, and the increasing, but already record income/wealth disparity in the United States and dramatic underperformance of everyone’s savings disproportionately invested in bonds will incite even more desperation.  Eventually if for some reason 2 and 3 do not kick in first, this desperation will become so severe that it will force investors to take risk.  Its exact manifestation is unknown, but it will appear somewhere other than bonds.  Overconfident and desperate risk-taking causes bubbles and since we have not seen any real risk-taking, no bubbles currently exist in stocks.

Data from [AAII- The American Association of Individual Investors](http://www.google.com/url?sa=t&source=web&cd=1&sqi=2&ved=0CBsQFjAA&url=http%3A%2F%2Faaii.com%2F&ei=BOIDTZq_H8OB8gbe36TrAg&usg=AFQjCNH43QiLqrZG9YBv_pvV1H-0qBeJoQ&sig2=Vdg0bSGYfr3vuS7SyBVw5w "AAII- The American Association of Individual Investors") and [ICI](http://www.google.com/url?sa=t&source=web&cd=1&ved=0CBoQFjAA&url=http%3A%2F%2Fwww.ici.org%2F&ei=6eADTa-EGYOBlAfowcmuDg&usg=AFQjCNHp-bkB5qtA4VrXR6oCgdo_7jq_Tw&sig2=Mb8QzLDFXlWir56i5jOCkA "ICI"):

[https://spreadsheets.google.com/ccc?key=0Amqp2r96khJPdENIRnE1SG5nanJ5OXFyYVUxOXRBVmc&hl=en](https://spreadsheets.google.com/ccc?key=0Amqp2r96khJPdENIRnE1SG5nanJ5OXFyYVUxOXRBVmc&hl=en "https://spreadsheets.google.com/ccc?key=0Amqp2r96khJPdENIRnE1SG5nanJ5OXFyYVUxOXRBVmc&hl=en")

For the R geeks:

require(quantmod)
require(ggplot2)

aaii_ici=read.csv("aaii-ici-noblank.csv",row.names=1)

#using ggplot example from [http://learnr.wordpress.com/2009/03/16/ggplot2-split-data-range-into-multiple-chart-series/](http://learnr.wordpress.com/2009/03/16/ggplot2-split-data-range-into-multiple-chart-series/)
p <- ggplot(data=aaii_ici, aes(x = AAIIBULL-AAIIBEAR, y = runSum(aaii_ici[,4],3), colour = Range, shape = Range, label = Range))
p1 <- p + geom_point() + scale_y_continuous(limits = c(-200000, 200000),formatter=comma) + geom_hline(yintercept=0) + geom_vline(xintercept=0) + stat_smooth(method="lm", se=FALSE) + ylab("ICI Equity Rolling 3-mo Sum") + opts(title = "ICI Equity Flows by AAII Survey")
print(p1)