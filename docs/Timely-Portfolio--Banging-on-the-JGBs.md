<!--yml

类别：未分类

日期：2024-05-18 15:00:17

-->

# Timely Portfolio: Banging on the JGBs

> 来源：[`timelyportfolio.blogspot.com/2013/04/banging-on-jgbs.html#0001-01-01`](http://timelyportfolio.blogspot.com/2013/04/banging-on-jgbs.html#0001-01-01)

由于我已经有段时间没有发过文章了，我想让大家知道我仍然活着并且很活跃。市场中的激情（机会）的复苏、季度报告周期以及难以置信的 R/javascript 发布的数量，让我没有时间写一些足够好以至于能发帖的东西。在市场中，日本和黄金让我笑逐颜开。在季度报告周期方面并没有什么特别新的东西，但我一直在密切关注[`axysreporting.com`](http://axysreporting.com)上的有趣想法，并且很高兴地学习了一些关于[`addepar.com`](http://addepar.com)的东西。不过，与过去两周内宣布的所有 R 和 javascript 包相比，它们都不足以让我印象深刻。我在我的帖子[d3 Lifeline from vega and clickme](http://timelyportfolio.blogspot.com/2013/04/d3-lifeline-from-vega-and-clickme.html)中提到了它们，但我忘记包括 Jeff Leek 的[Introducing the healthvis R package – one line D3 graphics with R](http://simplystatistics.org/2013/04/02/introducing-the-healthvis-r-package-one-line-d3-graphics-with-r)，他教了[`www.coursera.org/course/dataanalysis`](https://www.coursera.org/course/dataanalysis)，以及当时还未发布的[rCharts](http://ramnathv.github.io/rcharts)。[rCharts](http://ramnathv.github.io/rcharts)让我想起了我一直到现在都没有使用过的非常特别的[slidify](http://ramnathv.github.io/slidify)包。我**强烈、强烈地建议读者**仔细看看[**rCharts**](http://ramnathv.github.io/rcharts)和[**slidify**](http://ramnathv.github.io/slidify)。为了确保每个人都能看到这些，我重新列出了它们，并在下面添加了新的链接和 Twitter 公告。

> [vega](http://trifacta.github.io/vega)
> 
> 宣布 Vega，一种基于[#d3js](https://twitter.com/search/%23d3js)的新可视化语法！在 JSON 格式中设计可重用的图表组件[trifacta.github.com/vega](http://t.co/GuNbXu3jtv "http://trifacta.github.com/vega")
> 
> — Jeffrey Heer (@jeffrey_heer) [2013 年 4 月 2 日](https://twitter.com/jeffrey_heer/status/319109814926073857)
> 
> [rCharts](http://ramnathv.github.io/rcharts)同一个创建者作为[slidify](http://ramnathv.github.io/slidify/)
> 
> @[lisaczhang](https://twitter.com/lisaczhang)我写了一个 R 包，为 R 用户封装了 Polycharts 的功能。[ramnathv.github.io/rCharts](http://t.co/1Pcyp6E8wL "http://ramnathv.github.io/rCharts")
> 
> — Ramnath Vaidyanathan (@ramnath_vaidya) [2013 年 4 月 10 日](https://twitter.com/ramnath_vaidya/status/322127777669201920)
> 
> [clickme](http://github.com/nachocab/clickme)
> 
> @[xieyihui](https://twitter.com/xieyihui) 很想听听您对 clickme 的看法，这是一个使用[#knitr](https://twitter.com/search/%23knitr)填充 JS 可视化的 R 包[bitly.com/vizbi_clickme](http://t.co/zazjjM3tDo "http://bitly.com/vizbi_clickme")
> 
> — Nacho Caballero (@nachocaballero) [2013 年 3 月 24 日](https://twitter.com/nachocaballero/status/315652318123139072)
> 
> rhealthvis
> 
> 我们的包今天宣布了！[healthvis.org](http://t.co/iItsC0Snlh "http://healthvis.org")
> 
> — rhealthvis (@rhealthvis) [2013 年 4 月 2 日](https://twitter.com/rhealthvis/status/319096283711291392)

现在要展示我实验的一些结果，我在下面列出了一些 bl.ocks。这些所有数据的主要来源是日本政府债券(JGB)收益率数据，由[日本财务省](http://www.mof.go.jp/english/jgbs/reference/index.html)提供。我会在一个更详细的后续文章中讨论选择 JGB 的原因。我很乐意听听关于 JGB 和我的实验的看法。

1.  [`bl.ocks.org/timelyportfolio/5407807`](http://bl.ocks.org/timelyportfolio/5407807)  使用 clickme ractive 的日本政府债券(JGB)收益率小倍数图表

1.  [`bl.ocks.org/timelyportfolio/5405240`](http://bl.ocks.org/timelyportfolio/5405240)  带有 vega spec 和 clickme ractive 的日本政府债券(JGB)收益率曲线

1.  [`bl.ocks.org/timelyportfolio/5398614`](http://bl.ocks.org/timelyportfolio/5398614)  使用 clickme ractive 和 vega spec 的日本政府债券(JGB)收益率折线图

我的一些其他更基础的实验在这里。这些可能对还不熟悉这些新资源的人有所帮助。

1.  [`bl.ocks.org/timelyportfolio/5351448`](http://bl.ocks.org/timelyportfolio/5351448)

1.  [`bl.ocks.org/timelyportfolio/5342818`](http://bl.ocks.org/timelyportfolio/5342818)

1.  [`bl.ocks.org/timelyportfolio/5322390`](http://bl.ocks.org/timelyportfolio/5322390)

1.  [`bl.ocks.org/timelyportfolio/5316682`](http://bl.ocks.org/timelyportfolio/5316682)

我很快就会带来一个我希望非常令人印象深刻的由[slidify](http://ramnathv.github.io/slidify)创建的市场相关帖子。在此之前，请告诉我您的看法，或者展示您相关的实验。

感谢为这些伟大的开源项目付出辛勤努力每一个人。
