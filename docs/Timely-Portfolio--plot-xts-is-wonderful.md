<!--yml

类别：未分类

日期：2024-05-18 15:04:15

-->

# 及时投资组合：plot.xts 非常好用。

> 来源：[`timelyportfolio.blogspot.com/2012/08/plotxts-is-wonderful.html#0001-01-01`](http://timelyportfolio.blogspot.com/2012/08/plotxts-is-wonderful.html#0001-01-01)

如昨天 FOSS 交易帖子[A New plot.xts](http://blog.fosstrading.com/2012/08/a-new-plot-xts.html)中提到的。

> “[谷歌夏日代码（2012）](http://google-melange.appspot.com/gsoc/homepage/google/gsoc2012)项目为了[扩展 xts](http://rwiki.sciviews.org/doku.php?id=developers:projects:gsoc2012:xts)产生了一个非常 promising 的新 plot.xts 函数。迈克尔·韦兰德，项目的学生，写了[R-SIG-Finance](https://stat.ethz.ch/mailman/listinfo/r-sig-finance)来[请求印象、反馈和错误报告](http://draft.blogger.com/%20https://stat.ethz.ch/pipermail/r-sig-finance/2012q3/010652.html)。该函数位于[xtsExtra](https://r-forge.r-project.org/scm/viewvc.php/pkg/xtsExtra/?root=xts)包中，该包是[R-Forge 上的 xts 项目](https://r-forge.r-project.org/projects/xts)。
> 
> 请尝试 xtsExtra::plot.xts 并告诉我们您的想法。下面是迈克尔在[电子邮件](https://stat.ethz.ch/pipermail/r-sig-finance/2012q3/010652.html)中代码产生的视觉效果样本。当然，这不是一个单行样本，但它确实令人印象深刻！迈克尔，干得好！”

正如作者迈克尔·韦兰德在[`stat.ethz.ch/pipermail/r-sig-finance/2012q3/010652.html`](https://stat.ethz.ch/pipermail/r-sig-finance/2012q3/010652.html "https://stat.ethz.ch/pipermail/r-sig-finance/2012q3/010652.html")中宣布的。

> “作为最常用 xts 的社区，我想引起您对作为谷歌夏日代码 2012 的一部分可用的新 xts 对象绘图函数的注意。这项工作是对先前存在的 plot.xts 的重大改进，应该为您提供 R 中最全面和灵活的时间序列绘图。功能包括：
> 
> +   "automagic"布局构建和坐标轴对齐
> +   
> +   智能参数回收。
> +   
> +   面板函数能力。
> +   
> +   对 OHLC 对象更具吸引力的蜡烛和条形图
> +   
> +   散点图以查看多个序列的共同进化
> +   
> +   事件标记。
> +   
> +   政权突出。
> +   
> +   通过 barplot.xts [基于彼得·卡尔的代码]的时间导向条形图。
> +   
> +   与所有已知的 R 时间序列类实现互操作性，使用 xts 尝试/重新分类范式。
> +   
> 同时保留 plot.xts 提供的相同智能坐标格式和网格线。我们尽最大努力保持与旧 plot.xts 文档使用完全兼容，并与 plot.zoo 达到 95%的兼容性。我的目标是创建一个设计，使用智能默认值，让您随时随地都能拥有吸引人和信息丰富的图表，同时足够灵活，让“高级用户”可以按照自己的意愿制作每一个细节...”

迈克尔在这项谷歌编程之夏（GSOC）项目中做得非常出色，我期待着将 plot.xts 的所有新特性融入其中。作为一个与文章和邮件列表公告中展示的例子非常不同的快速示例，我认为展示我们如何使用 plot.xts 来替代 PerformanceAnalytics 包中的老前辈 chart.TimeSeries 和 charts.PerformanceSummary 图表将会很有趣。

对于 chart.TimeSeries，我将几乎完全复制文档中给出的图表。

并不是作为一个有用的应用，而是为了演示的需要，我们可以制作一些东西来区分样式，同时避免事件标签冲突（这是迈克尔在上个星期日晚上很晚才实施的功能）。

plot.xts 甚至允许 plot.zoo 和 lattice 面板类型的功能，这使我们能够做一些非常棒的事情，就像这个 charts.PerformanceSummary 风格的图表中所示。

我非常感激 R 语言社区所做出的这个非常有力的贡献。感谢所有参与其中的人。

[R 代码在 GIST 中（注意：从 R-forge 安装 xtsExtra）](https://gist.github.com/3373828)：
