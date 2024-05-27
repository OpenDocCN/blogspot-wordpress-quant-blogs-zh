<!--yml

分类：未分类

日期：2024-05-18 14:50:18

-->

# Timely Portfolio: Out of Nowhere–Explore Text on a Path

> 来源：[`timelyportfolio.blogspot.com/2014/12/out-of-nowhereexplore-text-on-path.html#0001-01-01`](http://timelyportfolio.blogspot.com/2014/12/out-of-nowhereexplore-text-on-path.html#0001-01-01)

我之前并没有真正停下来思考过这个问题，直到我听了这个[The Web Ahead podcast](http://5by5.tv/webahead/81)的节目，嘉宾是[Sara Soueidan](http://sarasoueidan.com)。科技界最有趣的现象之一就是专家似乎能从天而降，成为某个话题的权威。在这期节目中，接受采访的[Sara Soueidan](http://sarasoueidan.com)就是这样。我们可以在[Joni "Bologna" Trythall](http://jonibologna.com/portfolio/)的 SVG 例子中找到一个类似的例子。

我发现当我能将这些专家的内容融入到 R 中时，乐趣会更多。让我们像 Joni 在她的文章["Animating SVG text On A Path"](http://jonibologna.com/svg-text-along-a-path/)中那样，给文本沿着路径添加动画，不过我们用的是图表中的一条线。

<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 432 432" version="1.1"><text><textpath xlink:href="#ourline" startOffset="0.955991">some text on a path</textpath></text></svg>

我将复制下面的代码。如果需要教程，请让我知道。

````
library(SVGAnnotation)
library(pipeR)
library(htmltools)

# make as basic a line plot as I know how in R
svg = svgPlot(plot(sin(seq(0,pi*3,0.2)),type="l")) %>>%
  # extract the XML and use htmlParse
  # to overcome namespace confusion and difficulty
  saveXML %>>% htmlParse

# with base R plots, we get clues with clip-path attributes
# in this case we know with some inspection
# there will be one g with a clip-path attribute
# and that g will contain our plotted line
getNodeSet(svg,"//g[contains(@clip-path,'url')]//path")[[1]] %>>%
  # let's add an id so we can reference this later
  ( addAttributes( node=., id = "ourline" ) )

# first step in adding text to a path
# make a new text node
textOnPath = newXMLNode("text")
# now the critical part to join the text to the path
addChildren(
  textOnPath
  , newXMLNode(
    "textPath"
    ,attrs=c( "xlink:href" = "#ourline" ) #our id given above
    ,"some text on a path" #some very creative saying
  )
)

# add our text node to the svg plot
addChildren(
  getNodeSet(svg,"//svg")[[1]]
  ,kids = list(textOnPath)
)
# see if it works by sending to our viewer/browser
getNodeSet(svg,"//svg")[[1]] %>>%
  saveXML %>>% HTML %>>% html_print

# let's continue our journey by exploring the startOffset attribute
# startOffset says where on the path to start our text
# what happens if we add startOffset = 30%
getNodeSet(svg, "//textPath")[[1]] %>>%
  ( addAttributes( node = . , startOffset = "30%" ) )
# find out the effect of startOffset by browsing
getNodeSet(svg,"//svg")[[1]] %>>%
  saveXML %>>% HTML %>>% html_print

# for our grand finale we can animate the text
# note: this might not work in your browser, so use Chrome
# add a child animate node with the same attributes as Joni's tutorial
getNodeSet(svg, "//textPath")[[1]] %>>%
  (
    addChildren(
      node = .
      , newXMLNode(
        "animate"
        ,attrs = c(
          attributeName="startOffset"
          ,values = "0;0.7;1"
          ,dur = "8s"
          ,repeatCount = "indefinite"
          ,keyTimes = "0;0.2;1"
        )
      )
    )
  )
# see the animated text
getNodeSet(svg,"//svg")[[1]] %>>%
  saveXML %>>% HTML %>>% html_print(viewer=utils::browseURL)

````
