<!--yml

类别：未分类

日期：2024 年 05 月 18 日 15:28:10

-->

# OxyPlot，比特币进展等 | Tr8dr

> 来源：[`tr8dr.wordpress.com/2015/02/28/oxyplot-bitcoin-progress-etc/#0001-01-01`](https://tr8dr.wordpress.com/2015/02/28/oxyplot-bitcoin-progress-etc/#0001-01-01)

2015 年 2 月 28 日 · 下午 6:41

最近，我有点分心，与同事一起进行了一些与区块链相关的想法的头脑风暴，并且在研究和交易 UI 上工作。

**OxyPlot**

首先，我想为 OxyPlot 做个广告。如果你使用 F#/C#或.NET 生态系统，[OxyPlot](http://oxyplot.org "OxyPlot")是一个设计良好的交互式科学绘图库。该库支持 iOS、Android、Mono.Mac、GTK#、Silverlight 和 WPF。如果处理的数据量可控，强烈推荐使用[Bokeh](http://bokeh.pydata.org/en/latest/ "Bokeh")和 Python。但是，如果你需要大量的交互功能或需要与大型数据集交互，OxyPlot 是一个很好的解决方案：

![2015 年 2 月 28 日下午 6:00:14 的屏幕截图](https://tr8dr.wordpress.com/wp-content/uploads/2015/02/screen-shot-2015-02-28-at-6-00-14-pm.png)我想建立一个 UI，让我能够观察和发展对订单簿特征的更好直觉。OxyPlot 没有好的金融图表，所以我为项目贡献了高性能的交互式 K 线图和成交量图，可以处理数百万个柱（点），以及一些面板对齐控件。这是一个可以用 OxyPlot 组合的 UI 的示例：

![2015 年 2 月 28 日下午 5:53:31 的屏幕截图](https://tr8dr.wordpress.com/wp-content/uploads/2015/02/screen-shot-2015-02-28-at-5-53-31-pm.png)

**数据源状态**

我在等待 BTCChina 就其破损的 FIX 实现问题给我回复。由于 API 问题尚未解决，我实现了 BTC China 的 REST API，并为主要感兴趣的 4 个交易所部署了数据源：

![2015 年 2 月 28 日下午 6:23:18 的屏幕截图](https://tr8dr.wordpress.com/wp-content/uploads/2015/02/screen-shot-2015-02-28-at-6-23-18-pm.png)

尽管 2 个交易所需要 4 秒的采样（由于缺乏流 API），但在查询之间捕获了所有的中间交易。对于 L2 来源，通过观察订单簿连续快照之间产生差异的最小序列，可以推断出订单簿交易。所有数据源都产生了一个共同的交易格式：

![2015 年 2 月 10 日下午 6:33:12 的屏幕截图](https://tr8dr.wordpress.com/wp-content/uploads/2015/02/screen-shot-2015-02-10-at-6-33-12-pm.png)
