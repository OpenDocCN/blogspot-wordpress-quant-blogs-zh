<!--yml
category: 未分类
date: 2024-05-18 14:58:30
-->

# Timely Portfolio: ggplot2 meet d3

> 来源：[http://timelyportfolio.blogspot.com/2013/08/ggplot2-meet-d3.html#0001-01-01](http://timelyportfolio.blogspot.com/2013/08/ggplot2-meet-d3.html#0001-01-01)

With great libraries, just a couple lines of code can do amazing things.  For instance, let’s limit ourselves to less than 10 lines of code and see what ggplot2 and d3 can do.  We will use [gridSVG](http://sjp.co.nz/projects/gridsvg/) as discussed in yesterday’s post [I Want ggplot2/lattice and d3 (gridSVG–The Glue)](http://timelyportfolio.blogspot.com/2013/08/gridsvganother-glue-for-r-to-svg.html) to expose ggplot2 to d3.  Thanks [Hadley Wickham](https://twitter.com/hadleywickham), [Mike Bostock](http://bost.ocks.org/mike/), [Paul Murrell](https://www.stat.auckland.ac.nz/~paul/), [Simon Potter](http://sjp.co.nz/projects/gridsvg/), and [George Bull/Sharp Statistics](http://sharpstatistics.co.uk/r/ggplot2-guide/).

If the iframe does not appear below, click [here](http://timelyportfolio.github.io/gridSVG_panzoom/panzoom2_ggplot2.html).

**Just think what we can do if we remove our 10 line code limit.**

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