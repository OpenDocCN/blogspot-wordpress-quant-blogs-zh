<!--yml
category: 未分类
date: 2024-05-18 14:50:01
-->

# Timely Portfolio: Financial Charts | Pan and Zoom

> 来源：[http://timelyportfolio.blogspot.com/2015/02/financial-charts-pan-and-zoom.html#0001-01-01](http://timelyportfolio.blogspot.com/2015/02/financial-charts-pan-and-zoom.html#0001-01-01)

The [htmlwidget](http://htmlwidgets.org) for Week 2 over at [Building Widgets](http://buildingwidgets.com/blog) claims to add pan and zoom interactivity to almost all R charts.  Since their were no tests on financial charts, I thought I would try it out on a couple.  It really does work. 

Here is an example on an efficient frontier plotted from fPortfolio.

When we combine pipeR and htmlwidgets, we get a solid result from what I think is fairly elegant and understandable code.

```
svgPanZoom(
  svgPlot({
    returns %>>%
      (cumprod( 1 + . )) %>>%
      (.[endpoints(.,"months")]) %>>%
      ( ./lag(.,k=1) - 1 ) %>>%
      chart.SnailTrail(
        colorset = RColorBrewer::brewer.pal(9,"Set1")[-6]
        ,add.names="none"
        ,width = 36
        ,step = 36
        ,legend.loc = "topright"
      )
  },height= 10, width = 16)
)
```

An even more challenging test was chartSeries, and `svgPanZoom` still passed the test beautifully. See if it works on your machine.

```
 getSymbols("SPY")
svgPanZoom(svgPlot({chartSeries(SPY)},width = 12, height = 8)) 
```

If you would like to reproduce the plots, all the code is in this [Gist](https://gist.github.com/timelyportfolio/e2349d1e850313fcb1c6).