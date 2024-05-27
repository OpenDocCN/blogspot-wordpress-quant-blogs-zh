<!--yml

分类：未分类

date: 2024-05-18 14:58:39

-->

# Timely Portfolio: 我想要 ggplot2/lattice 和 d3（gridSVG–粘合剂）

> 来源：[`timelyportfolio.blogspot.com/2013/08/gridsvganother-glue-for-r-to-svg.html#0001-01-01`](http://timelyportfolio.blogspot.com/2013/08/gridsvganother-glue-for-r-to-svg.html#0001-01-01)

我非常喜欢交互式图表，尤其是当它们直接来自 R 时。我在[rCharts](http://rcharts.io/site)上发布了大量内容，但这不是唯一的方法。在我心中，有三种粘合剂可以将 R 与 SVG/HTML/JavaScript 链接起来：

1.  让 R 处理数据，然后将数据发送到 JavaScript 以创建 SVG 图形。这种过程被[rCharts](http://rcharts.io/site)、[clickme](http://rclickme.com/)、[d3network](http://christophergandrud.github.io/d3Network/)、[googleVis](http://cran.r-project.org/web/packages/googleVis/index.html)、[gigvis](https://github.com/rstudio/gigvis)和[tabplotd3](http://cran.r-project.org/web/packages/tabplotd3/index.html)采用。

1.  让 R 处理数据并生成图表，然后将 SVG 图形发送到 JavaScript 以实现交互性。[gridSVG](http://sjp.co.nz/projects/gridsvg/)和[SVGAnnotation](http://www.omegahat.org/SVGAnnotation/SVGAnnotationPaper/SVGAnnotationPaper.html#bib:SVGAnnotation)是两个例子，展示了如何实现这一点。

1.  使用 1 或 2，然后通过[shiny](http://rstudio.com/shiny)、[Rook](http://cran.r-project.org/web/packages/Rook/index.html)或其他类型的网络服务器接口，在 R 和 JavaScript 之间保持双向通信。

让我们考虑方法 2。R 有 ggplot2 和 lattice。JavaScript 有 d3。我想要两者都。

我们 R 用户非常依赖 ggplot2 和 lattice 引擎，这些引擎可以与任何语言的绘图库相媲美或超越。难道不好吗？[保罗·默雷尔](https://www.stat.auckland.ac.nz/~paul/)（ggplot2 和 lattice 的平台作者）编写了[gridSVG](http://sjp.co.nz/projects/gridsvg/)来实现这一点。[西蒙·波特](http://sjp.co.nz/projects/gridsvg/)在默雷尔的指导下，为他的荣誉项目完善了 gridSVG。现在它是一个功能齐全、健壮的包，能够将您最复杂的 ggplot2 和 lattice 杰作发送到 SVG。gridSVG 可以独立完成许多令人惊叹的事情，但我想将 gridSVG 与[d3](http://d3js.org)结合起来。点击[这里](http://timelyportfolio.github.io/gridSVG_intro)或下面的屏幕截图，了解如何将一点 gridSVG 胶水应用到 ggplot2 和 d3 上。

![image](http://timelyportfolio.github.io/gridSVG_intro)

感谢保罗·默雷尔、西蒙·波特、哈迪利·威克姆、迈克·博斯特克、邓肯·坦普尔 lang、黛博拉·诺尔顿、朱利安娜·威廉姆斯、安德烈亚斯·恩 umann、拉姆纳斯·瓦伊达纳特和其他许多人，是你们让这一切成为可能。
