<!--

分类：未分类

日期：2024-05-12 19:28:16

-->

# 量化交易：最大化复合收益率

> 来源：[`epchan.blogspot.com/2006/10/maximizing-compounded-rate-of-return.html#0001-01-01`](http://epchan.blogspot.com/2006/10/maximizing-compounded-rate-of-return.html#0001-01-01)

一个很少有交易员使用的简单公式

这里有一个小谜题，可能会难住许多职业交易员。假设某种股票表现出真正的（几何）随机游走，我的意思是该股票每分钟上涨 1%或下跌 1%的机会各占 50%。如果你买入这种股票，从长远来看，你最有可能是赚钱、亏钱，还是保本？

大多数交易员会脱口而出“平坦！”的答案，这是错误的。正确答案是你将每分钟亏损 0.5%的资金！这是因为对于几何随机游走，平均复合收益率不是短期（或一周期）收益率*m*（这里为 1%），而是*m - s²/2*，其中*s*（这里也为 1%）是短期收益率的标准差。这与几何平均数总是小于算术平均数的事实一致（除非数字相同，此时两个平均数相等）。当我们假设，像我这样做，收益率的算术平均数为零，几何平均数，它给出平均复合收益率，必然是负的。

这个量*m - s²/2*是选择最大增长策略的关键。在先前的文章（“[你应该使用多少杠杆](http://epchan.blogspot.com/2006/10/how-much-leverage-should-you-use.html)？”）中，我描述了一种通过杠杆最大化给定投资策略（即具有固定的*m*和*s*的策略）的长期增长率的方案。然而，我们通常面临的是具有不同预期回报和风险的不同策略的选择。我们如何在这它们之间进行选择？许多交易员认为我们应该选择具有最高夏普比率的那一个。如果交易员把他或她的每个赌注都保持在一个恒定的大小，这是合理的。但是，如果你是一个像先前的文章中提到的凯利投资者那样，致力于最大化长期财富的交易员，那么赌注的大小应该总是与复合回报成比例。最大化夏普比率并不能保证多周期回报的最大增长。最大化*m - s²/2*才能实现这一点。

进一步阅读：

米勒，斯蒂芬·J。《算术与几何平均不等式》。[ArithMeanGeoMean.pdf](http://www.math.princeton.edu/mathlab/book/papers/ArithMeanGeoMean.pdf)

夏普，威廉。《多周期回报》。[`www.stanford.edu/~wfsharpe/mia/rr/mia_rr3.htm`](http://www.stanford.edu/~wfsharpe/mia/rr/mia_rr3.htm)

*Poundstone, William. (2005). [财富公式](http://www.amazon.com/gp/redirect.html?ie=UTF8&location=http%3A%2F%2Fwww.amazon.com%2FFortunes-Formula-Scientific-Betting-Casinos%2Fdp%2F0809046377%2Fsr%3D8-1%2Fqid%3D1162737089%3Fie%3DUTF8%26s%3Dbooks&tag=quantitativet-20&linkCode=ur2&camp=1789&creative=9325) New York: Hill and Wang.*
