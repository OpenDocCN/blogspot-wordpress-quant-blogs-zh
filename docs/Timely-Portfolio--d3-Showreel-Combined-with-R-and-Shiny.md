<!--yml

类别：未分类

日期：2024-05-18 15:02:32

-->

# 及时作品集：结合 R 和 Shiny 的 d3 展示视频

> 来源：[`timelyportfolio.blogspot.com/2012/12/d3-showreel-combined-with-r-and-shiny.html#0001-01-01`](http://timelyportfolio.blogspot.com/2012/12/d3-showreel-combined-with-r-and-shiny.html#0001-01-01)

由于我上一次帖子中提供的 d3 示例[d3 和 r 通过 shiny 互动](http://timelyportfolio.blogspot.com/2012/12/d3-and-r-interacting-through-shiny.html)的部分非常薄弱，我想结合更有吸引力的[Showreel 示例](https://github.com/mbostock/d3/tree/master/examples/showreel)和同样的股票数据会很有趣。然而，这次数据将来自 R 的 getSymbols。另外，大多数图表使用累计回报数据会更好，所以我们用 R 将价格数据转换为累计回报序列。

本例中包含的代码几乎全部归功于[Mike Bostock](http://bost.ocks.org/mike/)，尽管现在代码已经所剩无几，但结构和想法属于[Trestle Technology 的 Jeff Allen](http://www.trestletechnology.net/2012/12/reconstruct-gene-networks/ "http://www.trestletechnology.net/2012/12/reconstruct-gene-networks/")。

在浏览器中实时查看[`glimmer.rstudio.com/timelyportfolio/shiny-d3-showreel/`](http://glimmer.rstudio.com/timelyportfolio/shiny-d3-showreel/)，所有代码[托管在 Github 上](https://github.com/timelyportfolio/shiny-d3-showreel)，请随意玩耍、实验，并让我知道您用这个做了哪些了不起的事情。

[`www.youtube.com/embed/IUZ5sJxoT0c?rel=0`](http://www.youtube.com/embed/IUZ5sJxoT0c?rel=0)

视频
