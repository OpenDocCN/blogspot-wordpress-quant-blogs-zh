<!--yml
category: 未分类
date: 2024-05-18 14:50:18
-->

# Timely Portfolio: Out of Nowhere–Explore Text on a Path

> 来源：[http://timelyportfolio.blogspot.com/2014/12/out-of-nowhereexplore-text-on-path.html#0001-01-01](http://timelyportfolio.blogspot.com/2014/12/out-of-nowhereexplore-text-on-path.html#0001-01-01)

I had not really stopped to think of this until I listened to this [The Web Ahead podcast](http://5by5.tv/webahead/81) with [Sara Soueidan](http://sarasoueidan.com).  What is really interesting about the tech world is how experts can seemingly pop up out of nowhere and become the authority on a topic.  In the podcast, this was the case with the interviewee [Sara Soueidan](http://sarasoueidan.com).  We can find a similar example in [Joni "Bologna" Trythall](http://jonibologna.com/portfolio/) with SVG.

I find it even more fun when I can incorporate these experts’ content into R.  Let’s animate some text on a path as Joni does in her article ["Animating SVG text On A Path"](http://jonibologna.com/svg-text-along-a-path/), but instead of an arbitrary path, let’s use a line in a plot.

<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 432 432" version="1.1"><text><textpath xlink:href="#ourline" startOffset="0.955991">some text on a path</textpath></text></svg>

I’ll copy the code below.  Let me know if a tutorial would be helpful.

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