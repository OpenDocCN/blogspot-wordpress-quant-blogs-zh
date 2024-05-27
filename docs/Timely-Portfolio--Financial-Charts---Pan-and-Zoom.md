<!--yml

分类：未分类

日期：2024-05-18 14:50:01

-->

# Timely Portfolio：财务图表 | 平移和缩放

> 来源：[`timelyportfolio.blogspot.com/2015/02/financial-charts-pan-and-zoom.html#0001-01-01`](http://timelyportfolio.blogspot.com/2015/02/financial-charts-pan-and-zoom.html#0001-01-01)

在[构建小部件](http://buildingwidgets.com/blog)的 Week 2 中的[htmlwidget](http://htmlwidgets.org)声称为几乎所有的 R 图表添加平移和缩放交互性。由于他们的财务图表上没有测试，我想尝试一下。它真的有效。

以下是一个从 fPortfolio 绘制的有效前沿的示例。

当我们结合 pipeR 和 htmlwidgets 时，我们从我认为相当优雅和易于理解代码中获得了坚实的成果。

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

更具挑战性的测试是 chartSeries，而`svgPanZoom`仍然通过了测试，非常出色。看看它是否在你的机器上工作。

```
 getSymbols("SPY")
svgPanZoom(svgPlot({chartSeries(SPY)},width = 12, height = 8)) 
```

如果你想要复制图表，所有的代码都在这个[Gist](https://gist.github.com/timelyportfolio/e2349d1e850313fcb1c6)中。
