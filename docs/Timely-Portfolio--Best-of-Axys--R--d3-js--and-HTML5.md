<!--yml

类别：未分类

日期：2024-05-18 15:05:22

-->

# 及时投资组合：Axys、R、d3.js 和 HTML5 最佳应用

> 来源：[`timelyportfolio.blogspot.com/2012/07/best-of-axys-r-d3js-and-html5.html#0001-01-01`](http://timelyportfolio.blogspot.com/2012/07/best-of-axys-r-d3js-and-html5.html#0001-01-01)

Axys、R、d3.js 和 HTML5 都为投资管理和报告提供了极其强大的工具，但它们并没有被设置为相互协同作用，以填补彼此的空白并相互利用对方的优势。在我的理想场景中，Axys 充当会计系统和性能计算器，R 充当高级金融/统计引擎，d3.js 充当互动报告组件，而 HTML5 提供用户界面，并通过 WebSockets 将所有内容紧密结合在一起（在这里很好地演示了 WebSockets：[`www.websocket.org/demos.html`](http://www.websocket.org/demos.html)）。在经历了 12 年的 Axys 工作之后，我很惊讶一切似乎都在顺利进行。我为 Axys 到 d3.js 在我的帖子[Axys 到 d3.js 错误捕获和格式化](http://timelyportfolio.blogspot.com/2012/07/axys-to-d3js-error-catching-and.html)中提供了一个简单的概念验证。现在让我们将其扩展到 R 和 WebSockets，通过慷慨捐赠的[R WebSockets 包](http://illposed.net/websockets.html)。我从作者在 YouTube 上展示的示例中借鉴了很多。

[`www.youtube.com/embed/0iR8Fo0jwW8`](http://www.youtube.com/embed/0iR8Fo0jwW8)

视频

在这个概念验证中，Axys 将计算性能并通过图表宏将其发送到 Excel，创建 JSON 和一个 html 页面（感谢 Bruce [`excelramblings.blogspot.com/`](http://excelramblings.blogspot.com/)）。html 页面包含 JavaScript 和 d3.js 以生成一个简单的条形图。现在我们在 Excel 中添加一个按钮，通过嵌入在 html 中的 JSON 将其发送到 R。R 将生成一个 charts.PerformanceSummary 图表，并将其作为 jpeg 发送回 html 页面。html 页面将接收图像，并用图像替换 d3.js 条形图。

[`www.youtube.com/embed/xC1daKifHvw`](http://www.youtube.com/embed/xC1daKifHvw)

视频

今后我将只使用 R 作为统计引擎，并继续依赖 d3.js 进行互动式报告。我走多远取决于用户的反馈。如果您希望我继续走这条路，请让我知道。

致谢名单开始变得很长。我衷心感谢 Mike Bostock 在 d3.js 上的出色工作[`github.com/mbostock/d3/wiki`](https://github.com/mbostock/d3/wiki "https://github.com/mbostock/d3/wiki")，R 包 PerformanceAnalytics 的 dedicated authors [`cran.r-project.org/web/packages/PerformanceAnalytics/index.html`](http://cran.r-project.org/web/packages/PerformanceAnalytics/index.html "http://cran.r-project.org/web/packages/PerformanceAnalytics/index.html")，Brian 作者的[`illposed.net/websockets.html`](http://illposed.net/websockets.html "http://illposed.net/websockets.html")和[示例](http://bigcomputing.com/PerformanceAnalytics.R)，RJSONIO 的作者[`cran.r-project.org/web/packages/RJSONIO/index.html`](http://cran.r-project.org/web/packages/RJSONIO/index.html "http://cran.r-project.org/web/packages/RJSONIO/index.html")，以及 Bruce McPherson 在[`excelramblings.blogspot.com/`](http://excelramblings.blogspot.com/ "http://excelramblings.blogspot.com/")的灵感想法。

为了自己解决问题，你需要 Excel 文件[cdataset.xlsm](https://www.box.com/s/ec9ddf33cefd5fd7cf10)，Axys 报告[perhstsp.rep](https://www.box.com/s/yhdagoqpznif8248etc5)，以及[GIST 上的 R 代码](https://gist.github.com/3145541)。
