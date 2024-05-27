<!--yml

分类：未分类

日期：2024-05-12 19:32:22

-->

# tornado 服务器，Bootstrap 客户端 | 编码市场

> 来源：[`etrading.wordpress.com/2014/10/07/tornado-server-bootstrap-client/#0001-01-01`](https://etrading.wordpress.com/2014/10/07/tornado-server-bootstrap-client/#0001-01-01)

## tornado 服务器，bootstrap 客户端

### 2024 年 5 月 12 日

去年四月份我[在我的博客上发过一篇关于使用 tornado 进行实时推送的文章](https://etrading.wordpress.com/2014/04/26/tornado-websockets/)，该文章讨论了如何使用[WebSocket](http://en.wikipedia.org/wiki/WebSocket)将实时数据推送到浏览器客户端。那时我正在构建一个概念验证（Proof of Concept, PoC）。自那时以来，我已经取得了很大的进步；我现在正在构建我产品的测试版。我仍在服务器端使用 tornado，并采用了 Twitter 的[Bootstrap](http://getbootstrap.com/)框架用于浏览器图形用户界面（GUI）。要熟练使用 Bootstrap 和[jQuery](http://jquery.com/)框架确实需要一定的学习曲线。但这是值得的，而且我对浏览器 GUI 开发在过去五年中的进步感到非常惊讶。不管怎样，本文的目的是推荐一个深入学习 tornado 服务器开发的优秀资源：[Oscar Vilaplana](http://oscarvilaplana.cat/)的[深入解析 Tornado - Europython 演讲](https://www.youtube.com/watch?v=4Ztq-Yz1ero)。这个 YouTube 视频的前几分钟没有声音，即使在那之后，音频也有点杂音。但请耐心观看。Oscar 花了一个小时引导大家通过基于 tornado 的代码及其支持的内核，并使其变得非常简单。他演讲中所有的示例都可以[在 bitbucket 上找到](https://bitbucket.org/grimborg/tornado-in-depth/src/tip/examples/)。感谢 Oscar！
