<!--yml

分类：未分类

日期：2024-05-18 05:00:31

-->

# Magmasystems 博客：SPlus、Adhoc 查询和 Coral8 公共窗口

> 来源：[`magmasystems.blogspot.com/2008/07/splus-adhoc-queries-and-coral8-public.html#0001-01-01`](http://magmasystems.blogspot.com/2008/07/splus-adhoc-queries-and-coral8-public.html#0001-01-01)

我正在读一篇

[Powerpoint 演示文稿](http://www.insightful.com/news_events/webcasts/2004/03zivot/HighFrequencyWebCast.pdf)

翻译：

Zivot

在

SPlus

，我对这个广告很感兴趣

hoc

查询设施，由 Eric 教授

SPlus

提供了很多功能。例如，如果你有

TAQ

将数据加载到

SPlus

，你可以使用以下的

SPlus

查询以获取 Microsoft 在一个非重叠的 5 分钟窗口内的平均价格：

平均值。5min = aggregateSeries(msftt.ts[,"Price"], + by="minutes",k.by=5,FUN=mean)

Coral8 最近实现了一个可查询的“公共窗口”，作为一种进行即席查询的方法。为了快速推出这个功能，Coral8 在系统中嵌入了一个 SQLite 版本。因此，你不能使用 Coral8 流式查询语言 CCL 进行窗口的即席查询。相反，你需要使用 SQL-92 的一个方言。

(Coral8 告诉我，最终你将能够使用 CCL 进行即席查询)

SPlus 看起来支持很多内置函数，用于时间序列金融数据。这也是我希望在 Coral8 中看到的东西。（我想也许有一个机会，可以围绕为资本市场公司增强 Coral8 建立一个小型的 cottage 工业...)

我想知道 CEP 供应商是否在决定使用流式 SQL 之前考虑过 SPlus/R 作为查询语言？（我知道 JOS 已经在 Barcap 的 R 大潮中有一段时间了。他最近虽然没有太多关于它的博客...)

©2008 Marc Adler - 版权所有。

这里的所有观点都是个人的，与我的雇主无关。
