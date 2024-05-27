<!--yml

类别：未分类

日期：2024-05-18 14:49:45

-->

# 及时投资组合：提取热图

> 来源：[`timelyportfolio.blogspot.com/2015/03/extracting-heatmap.html#0001-01-01`](http://timelyportfolio.blogspot.com/2015/03/extracting-heatmap.html#0001-01-01)

受此推文的启发，我想尝试在 JavaScript 中做类似的事情。

幸运的是，我找到了这篇旧帖子[R 图表+JavaScript 颜色](http://timelyportfolio.blogspot.com/2014/07/chart-from-r-color-from-javascript.html)作为参考，并且从这些链接中得到了很多帮助。

在几小时内，我完成了这个粗糙但可用的[渲染](http://timelyportfolio.github.io/rCharts_color_thief/index_jsfeat.html)，其中包括 d3.js 刷子来获取缩放。然后，由于这是一个金融博客，我想我们找到了一个旧的相关性热图，就像在[PIMCO 基金的美好相关性地图](http://timelyportfolio.blogspot.com/2012/06/pretty-correlation-map-of-pimco-funds.html)中一样。尽管我们可以猜测相关性值，但我认为获取实时值会更有趣。试试下面的功能。

1.  在缩放/图例上刷

1.  输入缩放最小值和最大值

1.  在图表中的颜色区域悬停

如我所说，这很粗糙，但能工作。它需要一点 UI 工作:)
