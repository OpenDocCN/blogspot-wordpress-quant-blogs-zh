<!--yml

category: 未分类

date: 2024-05-12 19:39:17

-->

# Web Workers | Coding the markets

> 来源：[`etrading.wordpress.com/2009/07/22/web-workers/#0001-01-01`](https://etrading.wordpress.com/2009/07/22/web-workers/#0001-01-01)

## Web Workers

### July 22, 2009

JavaScript GUI（如[Caplin Trader](http://www.caplin.com/caplintrader/)）所面临的一个严格限制是浏览器 JavaScript 引擎的单线程性。从[Comet server](http://www.freeliberator.com/documentation/)获取代码的异步执行，以便响应和及时地处理用户界面和网络事件，是相当困难的。

所以今天我很高兴看到了关于[Web Workers](http://ejohn.org/blog/web-workers/)的报道。在未来，它们将使像 Caplin Trader 这样的 GUI 能够在后台线程上处理网络事件…
