<!--yml

分类：未分类

日期：2024-05-18 15:04:35

-->

# 及时投资组合：基础图形中的地平线图

> 来源：[`timelyportfolio.blogspot.com/2012/08/horizon-plots-in-base-graphics.html#0001-01-01`](http://timelyportfolio.blogspot.com/2012/08/horizon-plots-in-base-graphics.html#0001-01-01)

对于背景，请参见先前的帖子 [关于地平线图表的更多内容](http://timelyportfolio.blogspot.com/2012/08/more-on-horizon-charts.html)， [地平线图的应用](http://timelyportfolio.blogspot.com/2012/07/application-of-horizon-plots.html)， [地平线图已经可用](http://timelyportfolio.blogspot.com/2012/06/horizon-plot-already-available.html)， [以及](http://timelyportfolio.blogspot.com/2012/06/cubism-horizon-charts-in-r.html) [R 中的立体主义地平线图表](http://timelyportfolio.blogspot.com/2012/06/cubism-horizon-charts-in-r.html)

在 R 中主要有三种图形途径（基础图形、网格图形和 ggplot2），每种都有它们的狂热者。 上次在 [关于地平线图表的更多内容](http://timelyportfolio.blogspot.com/2012/08/more-on-horizon-charts.html) 中，我使用了网格图形和网格图形扩展。 这次我们将使用基础图形建立地平线图，我对结果很满意。 ~~不幸的是，有一个小问题，即正数到负数的点的变化重叠。 如果您有解决方案，请告诉我。~~ *感谢有益的读者提供他们的评论和代码更改，现在这个问题已经解决了。*

现在，让我们来实现一个 for 循环并将负值镜像。

使用基础图形中的地平线图功能，希望我们现在可以将其添加到其他包中。 下面是一个使用 quantmod 的潜在示例。

[R 代码在 GIST 中（为了复制/粘贴，请使用原始格式）](https://gist.github.com/3247653)
