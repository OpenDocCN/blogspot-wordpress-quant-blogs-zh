<!--yml
category: 未分类
date: 2024-05-18 14:51:19
-->

# Timely Portfolio: SVG + a little extra (d3.js) in RStudio Browser | No Pipes This Time

> 来源：[http://timelyportfolio.blogspot.com/2014/10/svg-little-extra-d3js-in-rstudio.html#0001-01-01](http://timelyportfolio.blogspot.com/2014/10/svg-little-extra-d3js-in-rstudio.html#0001-01-01)

I’m guessing here, but yesterday’s post [Responsive SVG in Your RStudio Browser](http://timelyportfolio.blogspot.com/2014/10/reponsive-svg-in-your-rstudio-browser.html) might have inspired some “but,…)”s, “yes plus I need”s, “what the %>>% with the pipe”s, etc.  I’ll attempt to address a couple of these in this quick post.

First, if you don’t like pipes, here is the non-piped version of the code.  I also made one change, which assumes that you want the SVG to fill the <div> container.  This is helpful if you think you will only have one plot and nothing else in your HTML.

```
library(SVGAnnotation)
library(htmltools)

respXML <- function( svg_xml, height = NULL, width = "100%", print = T, ... ){
  # svg_xml should be an XML document
  library(htmltools)
  library(XML)

  svg <- structure(
    ifelse(
      length(getDefaultNamespace(svg_xml)) > 0
      ,getNodeSet(svg_xml,"//x:svg", "x")
      ,getNodeSet(svg_xml,"//svg")
    )
    ,class="XMLNodeSet"
  )

  xmlApply(
    svg
    ,function(s){
     a = xmlAttrs(s)
     removeAttributes(s)
     xmlAttrs(s) <- a[-(1:2)]
     xmlAttrs(s) <- c(
       style = paste0(
         "height:100%;width:100%;"
       )
     )
    }
  )

  svg <- HTML( saveXML( svg_xml) )

  svg <- tags$div(
      style = paste(
        sprintf('width:%s;',width)
        ,ifelse(!is.null(height),sprintf('height:%s;',height),"")
      )
      ,svg
    )

  if(print) html_print(svg) 

  return( invisible( svg ) )
}

```

Second, I like it but I’m helpless without my Javascript helper libraries, such as [d3.js](http://d3js.org), [Snap.svg](http://snapsvg.io), [Raphaël](http://raphaeljs.com/), etc.  htmltools makes it fairly easy to attach dependencies.  Let’s add [d3.js](http://d3js.org) in this example.

Third, I want to use my helper library to add some script to make something awesome.  I can’t help with the awesome part, but I can show you how to add a little bit of code.  This time we’ll take the simple pan/zoom code from [ggplot2 meet d3](http://timelyportfolio.blogspot.com/2013/08/ggplot2-meet-d3.html), and here is the result.  Please understand that this is only 4 lines of Javascript, so the pan/zoom is not nearly as refined as I would expect.

[![R_svg_d3js](img/84427a1c63c1ae0b0bd07b4a521eb608.png "R_svg_d3js")](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjOjxJKoUPuHkTNp1fN8YnvUX3SJ7SWRuY0ph7pVfZdh6HevzkAUAxPMrOAgK7Ycv3L3cF4BxHYdqf4c42CKA0ZE7DaJ8JG24bHolXsA3u82jZ-q_K4bgcGLznFPPD4XgVplw5d-L_uxA/s1600-h/R_svg_d3js%25255B4%25255D.gif)

```
# make our plot here
# since we will need to manipulate to add a g container
# for smoother d3 pan/zoom
sP = respXML( 
  svgPlot(
    dotchart(
      t(VADeaths)
      , xlim = c(0,100)
      , main = "Death Rates in Virginia - 1940"
    )
  )
  , height = "100%"
  , print = F
)

# parse the plot html with rvest
sP = html(as.character(sP))
# add a g node to contain the plot
#  for smoother d3 pan / zoom
g = newXMLNode("g")
# add the old g to our new g container
addChildren(g, html_nodes(sP,"svg > g"))
# add our new g container to our svg
addChildren(html_nodes(sP,"svg")[[1]],g)

html_print(attachDependencies(
  tagList(
    # get the div with our modified svg
    HTML(saveXML(html_nodes(sP,"div")[[1]]))
    , tags$script(
      HTML(
        '
        var g = d3.select("svg > g");
        var zoom = d3.behavior.zoom().scaleExtent([1, 8]).on("zoom", zoomed)
        g.call(zoom)

        function zoomed() {
          g.select("g")
            .attr(
              "transform",
              "translate(" + d3.event.translate + ")scale(" + d3.event.scale + ")"
            );
        }
        '
      )
      )
      )
  ,htmlDependency(
    name="d3"
    ,version="3.0"
    ,src=c("href"="http://d3js.org/")
    ,script="d3.v3.js"
  )
      ))
```