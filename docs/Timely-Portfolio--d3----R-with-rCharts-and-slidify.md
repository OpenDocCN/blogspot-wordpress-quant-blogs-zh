<!--yml

category: 未分类

date: 2024-05-18 15:00:13

-->

# [及时投资组合：通过 rCharts 和 slidify 连接 d3 和 R](http://timelyportfolio.github.io/rCharts_512paths/)

> 来源：[`timelyportfolio.blogspot.com/2013/04/d3-r-with-rcharts-and-slidify.html#0001-01-01`](http://timelyportfolio.blogspot.com/2013/04/d3-r-with-rcharts-and-slidify.html#0001-01-01)

我相信《纽约时报》的互动特性[512 条通往白宫的道路](http://www.nytimes.com/interactive/2012/11/02/us/politics/paths-to-the-white-house.html?_r=0)是史上最棒的可视化之一。当我们了解到这个奇迹的[创作过程](http://chartsnthings.tumblr.com/post/35616801795/some-sketches-from-the-times-scenario-builder)时，它变得更加出色。尽管这个图表不适用于其他数据源（如果这个说法不正确，请告诉我），但我无法抗拒使用 Ramnath Vaidyanathan 的 R 包[slidify](http://slidify.org)和[rCharts](https://github.com/ramnathv/rCharts)来从 R 中构建它。在看到他的教程[复制纽约时报互动图表](http://ramnathv.github.io/rChartsNYT/)和他的演示[可视化雷哈特和罗戈夫的公共债务研究](http://glimmer.rstudio.com/ramnathv/rChartsRogoff/)之前，我甚至认为这不可能。

> 我有一种感觉，到 2013 年底，几乎每个使用 lattice 或 ggplot2 的 R 用户都会对 Ramnath 的才华有所了解。他甚至可能会说服一些 d3 用户尝试一下 R。

更加令人惊叹的是，下面整个教程（如果无法显示，请点击[这里](http://timelyportfolio.github.io/rCharts_512paths/)）都是使用 R 和[slidify](http://slidify.org)创建的，因此完全可以复现。尽管 rCharts 还处于早期开发阶段，但我强烈建议您尝试一下。
