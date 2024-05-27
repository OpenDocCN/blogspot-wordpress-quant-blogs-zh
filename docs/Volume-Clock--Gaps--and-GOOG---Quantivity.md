<!--yml

category: 未分类

date: 2024-05-18 13:44:19

-->

# Volume Clock, Gaps, and GOOG | Quantivity

> 来源：[`quantivity.wordpress.com/2012/10/23/volume-clock-gaps-and-goog/#0001-01-01`](https://quantivity.wordpress.com/2012/10/23/volume-clock-gaps-and-goog/#0001-01-01)

GOOG 在上周早些时候意外地披露了他们的 Q3 收益，即 10 月 18 日。尽管收益略显有趣，但更有趣的是日内交易中的相应小插曲。这一事件为深入研究 TAQ 数据、通过 HFT 的视角来观察，并从 Mendelbrot、Clark 和 Ané的一些优雅观点中建立直觉提供了机会。

首先看一下 18 日 GOOG 的日内交易价格的时间序列图（来自一个交易所）：

![](https://quantivity.wordpress.com/wp-content/uploads/2012/10/goog-trades-20121018.png)

该磁带清楚地说明了一些不愉快的交易者，午间似乎出现了跳空下跌（后来交易停牌直到下午 3 点）。通过相应交易和报价的时间序列摘要，可以更好地理解日内动态：

![](https://quantivity.wordpress.com/wp-content/uploads/2012/10/goog-taq-20121018.png)

尽管从低频日线图中查看时价格似乎有所间隙，但在午间时段深入观察表明相反：

![](https://quantivity.wordpress.com/wp-content/uploads/2012/10/goog-taq-20121018-noon-one.png)

与其说是单次打印间隙，不如说是价格行为在 12:30 至 12:40 之间较缓慢地演变。预计是由于披露后交易量的增加而推动，12:30 后价格迅速扩大。12:32 后不久即印出了一笔 5000 股的交易，当时价差开始稳定。这引发了一些恐惧和贪婪，因为做市商将价差扩大到了 4 美元。中午后价差动态似乎是对不确定性和毒性的典型反应，因为该摘要在质量上与其他类似事件（如 2008 年熊市后的早晨）相似。

作为对比，以下是 TAQ 摘要在下午 3:25 - 4 点的图表：

![](https://quantivity.wordpress.com/wp-content/uploads/2012/10/goog-taq-20121018-three-four.png)

现在我们已经熟悉了以人类年表为单位衡量的 TAQ 行动，让我们通过不同的视角来看待它——根据 Mandelbrot（1963）、Clark（1971）以及最近的 Easley 等人（2012）的直觉。

要做到这一点，首先考虑另一天（更正常的一天）的谷歌（GOOG）交易，比如说接下来的 10 月 19 日。从人类时间学角度出发，计算 1 分钟和 5 分钟柱状图的第一差分的时间序列。然后从第一差分中估算[Epanechnikov 核密度](http://en.wikipedia.org/wiki/Kernel_density_estimation)。最后，对于相同的第一差分，拟合相应的高斯分布。或者，在 R 中：

```

# first differences
min1Diff <- diff(to.minutes(trades$price)[,4], na.pad=F)
min10Diff <- diff(to.minutes5(trades$price)[,4], na.pad=F)

# kernel densities
min1Density <- density(min1Diff, kernel="epanechnikov")
min10Density <- density(min10Diff, kernel="epanechnikov")

# corresponding normals
min1Normal <- fitdistr(coredata(min1Diff), "normal")$estimate
min10Normal <- fitdistr(coredata(min10Diff), "normal")$estimate

```

下面是 10 月 19 日的图表，实线红色为 1 分钟差分密度，实线蓝色为 5 分钟差分柱状图（现在忽略黑色）；相同差分的高斯拟合为虚线：

![](https://quantivity.wordpress.com/wp-content/uploads/2012/10/goog-clock-20121019.png)

这重现了高频率回报的熟悉的风格化分布，与 Clark（1971）的图 1 和 Easley 等人（2012 年）的附件 2 一致。尽管肯定是尖峰状的，但这些分布与正态分布并没有太大不同。

现在，忽略时间上的顺序，而是从*基于一天内交易的股票量的时钟*的角度考虑交易。换句话说，生成一个新的过程，定义为与一天内总交易量相等大小的股票交易的价格序列相吻合的序列。这个过程为交易生成了一个“量时钟”，在这样做的过程中展示了一个美丽的时间序列转换。

可以从交易量时钟中估算出类似的核密度，以上图中黑色绘制（虚线对应的正态拟合），假设分区大小为 50。这展示了与 Easley 等人（2012 年）的附件 2 一致的分布特征。

有了对量时钟密度的直觉，我们最终可以通过以下图表从计算机的角度来看待 10 月 18 日：

![](https://quantivity.wordpress.com/wp-content/uploads/2012/10/goog-clock-20121018.png)

不用说，10 月 18 日的这个图与前一天 10 月 19 日的图完全不同。尤其有趣的是，5 分钟柱状图（蓝色）和交易量时钟（黑色）的正常拟合，它们与相应的核密度估计几乎没有相似之处。在看起来像这样的日子进行交易需要谨慎。

对于那些想要了解更多的人，请参阅 Clark（1971）以了解理论，包括从属随机过程（最初由 Bochner（1960）提出）。Ané和 Geman（2000）应用了更多的复杂性，包括辩论支持累积交易次数而不是累积交易量。也许值得进行后续帖子以查看这是否仍然合理，考虑到目前主要是算法性程序交易的时代。

生成上述图表的 R 代码是：

```

plot(trades20121018$price, main="GOOG Trades (2012-10-18)")
plotTAQSummary("GOOG", "2012-10-18", as.POSIXct("2012-10-18 09:30:00"), as.POSIXct("2012-10-18 16:05:00"))
plotTAQSummary("GOOG", "2012-10-18 | 12:00 - 13:00", as.POSIXct("2012-10-18 12:00:00"), as.POSIXct("2012-10-18 13:00:00"))
plotTAQSummary("GOOG", "2012-10-18 | 15:00 - 16:00", as.POSIXct("2012-10-18 15:25:00"), as.POSIXct("2012-10-18 16:05:00"))
plotTimeChangeDensity("GOOG", as.Date("2012-10-19"), trades20121019)
plotTimeChangeDensity("GOOG", as.Date("2012-10-18"), trades20121018)

```

并且，关于从属过程、量时钟和价格过程的一些文献：

+   Bochner，《调和分析与概率论》，加州大学出版社，伯克利，1960 年。

+   Mandelbrot，《某些投机价格的变动》，《商业杂志》，第 36 卷（1963 年），第 394-419 页。

+   Clark，《具有有限方差的下位随机过程模型用于投机价格》，经济研究中心，明尼苏达大学，1971 年。

+   Ané 和 Geman，《订单流量、交易时钟和资产收益的正态性》，《金融杂志》，第 55 卷，第 5 期（2000 年），第 2259-2284 页。

+   Murphy 和 Izzeldin，《订单流量、交易时钟和资产收益的正态性：Ané 和 Geman（2000 年）的再访》，2006 年。

+   Easley、de Prado 和 O’Hara，《成交量时钟：对高频范式的洞见》，《投资组合管理杂志》，2012 年 5 月。
