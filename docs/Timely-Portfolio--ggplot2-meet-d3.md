<!--yml

category: 未分类

date: 2024-05-18 14:58:30

-->

# Timely Portfolio: ggplot2 遇见 d3

> 来源：[`timelyportfolio.blogspot.com/2013/08/ggplot2-meet-d3.html#0001-01-01`](http://timelyportfolio.blogspot.com/2013/08/ggplot2-meet-d3.html#0001-01-01)

有了强大的库，只需几行代码就能完成惊人的事情。例如，让我们限制自己在 10 行代码以内，看看 ggplot2 和 d3 能做些什么。我们将使用[gridSVG](http://sjp.co.nz/projects/gridsvg/)，正如昨天帖子[我想要 ggplot2/lattice 和 d3 (gridSVG–粘合剂)](http://timelyportfolio.blogspot.com/2013/08/gridsvganother-glue-for-r-to-svg.html)中讨论的那样，将 ggplot2 暴露给 d3。感谢[Hadley Wickham](https://twitter.com/hadleywickham)，[Mike Bostock](http://bost.ocks.org/mike/)，[Paul Murrell](https://www.stat.auckland.ac.nz/~paul/)，[Simon Potter](http://sjp.co.nz/projects/gridsvg/)和[George Bull/Sharp Statistics](http://sharpstatistics.co.uk/r/ggplot2-guide/)。

如果下面的 iframe 没有出现，请点击[这里](http://timelyportfolio.github.io/gridSVG_panzoom/panzoom2_ggplot2.html)。

想象一下如果我们摒弃了 10 行代码的限制，我们能做些什么吧。**

```
#get the latest version of gridSVG
#install.packages("gridSVG", repos="http://R-Forge.R-project.org")

require(ggplot2)
require(gridSVG)

#draw a ggplot2 graph
#thanks http://sharpstatistics.co.uk/r/ggplot2-guide/
p <- ggplot(iris, aes(Sepal.Length, Sepal.Width)) + geom_point()
p + facet_grid(. ~ Species) + stat_smooth(method = "lm")

#define a simple html head template
htmlhead <- 
'<!DOCTYPE html>
<head>
  <meta charset = "utf-8">
  <script src = "http://d3js.org/d3.v3.js"></script>
</head>

<body>
'

#use gridSVG to export our plot to SVG
mysvg <- grid.export("panzoom1.svg")

#define a simple pan zoom script using d3
panzoomScript <-
'  <script>
    var svg = d3.selectAll("#gridSVG");
    svg.call(d3.behavior.zoom().scaleExtent([1, 8]).on("zoom", zoom))

    function zoom() {
      svg.attr("transform", "translate(" + d3.event.translate + ")scale(" + d3.event.scale + ")");
    } 
  </script>
</body>
'

#combine all the pieces into an html file
sink("panzoom_ggplot2.html")
cat(htmlhead,saveXML(mysvg$svg),panzoomScript)
#close our file
sink(file=NULL)

```
