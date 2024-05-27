```yml

分类：未分类

日期：2024-05-18 15:05:10

```

# Timely Portfolio: Hi R and Axys, I’m d3.js “Nice to Meet You” (On the Iphone)

> 来源：[`timelyportfolio.blogspot.com/2012/07/hi-r-and-axys-im-d3js-nice-to-meet-you.html#0001-01-01`](http://timelyportfolio.blogspot.com/2012/07/hi-r-and-axys-im-d3js-nice-to-meet-you.html#0001-01-01)

我仍然处于概念验证阶段，但随着我取得进展，我越来越对将 d3.js 与 R 和 Axys 结合起来的前景感到兴奋，这是通过 Bryan Lewis 的非常好的 R websockets 包实现的（现在他增加了 daemonize 函数，变得更加出色）。在这个迭代中，我将添加一个累计增长折线图，一些动画和过渡效果，然后 JavaScript 将要求 R 计算回撤。上次 R 返回的是一个图表，这次 R 将通过 JSON 通过 websocket 发送回撤计算的结果。然后我们使用 d3.js 绘制回撤的折线图。当我们考虑到现有的以及[感谢 Google Summer of Code 很快将增加的](http://www.google-melange.com/gsoc/project/google/gsoc2012/matthieu_ensimag/26001)风险/回报计算，由 R PerformanceAnalytics 包提供的计算，这变得非常强大。

视频的最后还有一个额外的奖励，那就是我们可以通过 iPhone 和 iPad 获得这种交互式的报告体验和 websocket 通信。

作为一个简单的回顾，正在发生的事情

1.  Axys 运行一个名为 perhstsp.rep 的报告。

1.  Axys 调用 cdataset.xlsm testd3axys 宏并发送性能信息。

1.  Excel cdataset.xlsm testd3axys 宏进行一些非常基本的格式化，将数据转换为 JSON，创建一个网页，然后在默认浏览器中打开该网页。

1.  浏览器打开网页，然后 d3.js 生成一个性能条形图，然后是一个累计增长折线图。

1.  浏览器提供了一个按钮，用于打开与 R 的 websocket 连接，并发送最初在 Axys 中计算的性能信息。

1.  R 通过 websocket 接收性能数据，计算回撤，然后将回撤计算结果作为 JSON 发送回浏览器。

1.  浏览器接收到回撤计算，然后 d3.js 将它们绘制成折线图。

[`www.youtube.com/embed/jz0cpO3Kp4Q`](http://www.youtube.com/embed/jz0cpO3Kp4Q)

VIDEO

下一组迭代将重点关注清理 d3.js 图表并添加交互性。

到目前为止，我还没有收到任何评论。请告诉我你们对这方面的看法。

致谢名单越来越长了。我非常感谢 Mike Bostock 在 d3.js 上的出色工作[`github.com/mbostock/d3/wiki`](https://github.com/mbostock/d3/wiki "https://github.com/mbostock/d3/wiki")，R 包 PerformanceAnalytics 的 dedicated 作者们[`cran.r-project.org/web/packages/PerformanceAnalytics/index.html`](http://cran.r-project.org/web/packages/PerformanceAnalytics/index.html "http://cran.r-project.org/web/packages/PerformanceAnalytics/index.html")，Bryan，他撰写了[`illposed.net/websockets.html`](http://illposed.net/websockets.html "http://illposed.net/websockets.html")以及[示例](http://bigcomputing.com/PerformanceAnalytics.R)，RJSONIO 作者[`cran.r-project.org/web/packages/RJSONIO/index.html`](http://cran.r-project.org/web/packages/RJSONIO/index.html "http://cran.r-project.org/web/packages/RJSONIO/index.html")，以及为这个灵感提供支持的 Bruce McPherson 在[`excelramblings.blogspot.com/`](http://excelramblings.blogspot.com/ "http://excelramblings.blogspot.com/")。

为了独立完成工作，你需要 Excel 文件[cdataset.xlsm](https://www.box.com/s/ec9ddf33cefd5fd7cf10)，Axys 报告[perhstsp.rep](https://www.box.com/s/yhdagoqpznif8248etc5)，以及来自 GIST 的[R 语言代码](http://bl.ocks.org/3190664)。
