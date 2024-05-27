<!--yml

category: 未分类

date: 2024-05-12 20:03:37

-->

# Falkenblog: Now Not the Time to Value-Tilt Low Vol

> 来源：[`falkenblog.blogspot.com/2013/08/now-not-time-to-value-tilt-low-vol.html#0001-01-01`](http://falkenblog.blogspot.com/2013/08/now-not-time-to-value-tilt-low-vol.html#0001-01-01)

Every week, a low volatility researcher has the same epiphany:

*tilt low volatility towards value.*

This addresses two pressing issues simultaneously: avoiding overbought securities and adding value alpha.

A neat articulation of this view is from Feifei Li of Research Affiliates,

[who first shows](http://www.researchaffiliates.com/Our%20Ideas/Insights/Fundamentals/Pages/S_2013_07_Avoiding-Pricey-Low-Volatility-Investing.aspx)

that lots of people are investing in low volatility (there's another such piece

[here](http://www.imw.tuwien.ac.at/fileadmin/t/imw/ibwl/dangl/MinVar.pdf?goback=%2Egde_3326656_member_263684291)

by Dangle and Kashofer from Vienna UofT). Clearly growth in low volatility is rising exponentially, and our intuition senses a Malthusian endgame that will be nasty and brutish.

That might seem scary, but to put it in perspective, there's now $80B in

*value ETFs*

alone, so this isn't anywhere close to value and size. Next, she shows some valuation metrics.  Three different types of low vol portfolios are seemingly higher priced using two different value metrics, book/market and earnings yield.  That is, low vol portfolios over the past 10 years used to have higher earnings yields than the market, and higher book/market ratios; now it's the reverse.

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjRjn2vcO9QrBItfyI9ces34pw2KsgDeRWFImHoX-ZGOHdrUxTdWxyHUj00GXgY5Xie8oZk9NXceD1faCwn44wczErhHyR9KNTAmPQgKiv7ebLjEWSJDl0PK8s75eArN8-CQjvHOA/s1600/fifi2.jpg)

To put these into perspective, the relative difference in the book-to-price ratio moving from 0.3 to 0.6 is about moving from the 15th percentile to the 45th percentile.  Li suggests adding a valuation criteria to low volatility to counteract this value-creep. The basic idea is, say the book/market ratio has a linear relation with expected return, where a higher book/market is associated with a higher return.  So if we take the universe of a set of low vol stocks, say the constituents of the ETF SPLV, which looks a the 100 least volatile stocks of the past year, and then take those stocks with the highest book/market ratios within that set, we simultaneously capture more of the value effect

**and**

avoid overbought stocks. That seems like a win-win improvement.

There are two problems with this approach.  First, the return to the book/market is not linear.  Therefore, merely moving your average book/market ratio may may you feel better, but unless you pick the right stocks, you won't change much.  Here's the average return by book/market deciles, for those stocks above the 20th percentile of the NYSE (all data here are from Ken French's excellent

[网站](http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html)

，我使用第 20 百分位数作为截止点，因为低于这个水平的股票实际上没有办法进行规模投资，所以可能会有误导)。

现在，这些是高于市场平均水平的平均月度回报溢价。 如果我们看几何回报率，那么顶部十分位的急剧增加并不存在，但现在先忘记这些（我认为几何平均值更相关，因为在实践中人们并不每月重新平衡，但这是每个人的选择）。 关键是，这种关系发生在可投资的宇宙的末端十分位，而不是之间。 因此，账面/市值十分位的平均数可能会误导人，因为在 30%到 90%的百分位之间几乎没有什么发生。

有趣的是，市值并没有均匀分配在所有十个账面/市值十分位上，因为大小和账面/市值排序的截止点

[每年利用纽约证券交易所构建。](http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/Data_Library/det_100_port_sz.html)

例如，目前，账面/市值第 1 十分位的市值约为账面/市值第 10 十分位的 3 倍。

这里是市值加权平均的账面/市值十分位数随时间变化的情况（蓝色标注）。 我在这里只是计算了法国数据中的一个数字，所有的工作都在

[这个 Excel 电子表格](http://www.efalken.com/valueFactor.xlsx)

（这里没有任何专有内容）。 所以这里是每个月计算的平均数字，以及法国价值因子的总回报（也就是 HML，或者高减低因子组合的替代投资组合）。 

显然，低平均账面/市值十分位对 HML 因子回报的增长有明显影响。 如果我把时间序列拆分成十分位并将数据放入其中，我可以清楚地看到未来 HML 回报的一个清晰的模式：

基本上，价值（即 HML）因子只有当平均账面/市值十分位在其分布的最低三分之一时才能获得回报。 遗憾的是，现在我们并不满足这一条件，我们现在约在 70 个百分位上。 所以，这里是价值因子的平均回报，针对目前（平均账面/市值十分位在总体平均值以上的情况下的 50%）：

那条线是倾斜的

*错误的做法*

如果你依赖价值溢价。

总的来说，为了提高低波动性而大量注重价值因子是危险的，因为 1）账面/市值与回报之间的关系并不是线性的，所以简单的投资组合平均数可能会误导人，2）鉴于市场在账面/市值十分位上的分布，价值溢价可以可预测地预测。

在实践中，自 1990 年左右才开始流行的被动指数的价值溢价大约为 1-2%。 而从 1928 年到 2013 年的 2.8% HML 溢价在很大程度上是由

*做空*

低账面/市值股票，这是一个可疑可行性的溢价，因此这个数字不能成为向价值倾斜的良好经验法则。 像价值 ETF 这样的

[IWD](http://finance.yahoo.com/q?s=iwd&ql=1)

大约在 2000 年左右偶然出现，因此它们每年的 3%超额收益都来自互联网泡沫的破裂 - 如果那些价值 ETF 回溯到 1990 年，回报溢价就会更少。我会估计价值因子有 100 个基点，但这仅仅是自身的。当你尝试使用价值来增加其他策略时，显然并不是有利的，而大多数低波动从业者都在这样做，所以你真的没有在打破思维定式。
