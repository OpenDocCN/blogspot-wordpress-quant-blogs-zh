<!--yml

分类：未分类

日期：2024-05-18 05:53:38

-->

# 复用与 WebSocket | 交易桌面故事

> 来源：[`mdavey.wordpress.com/2014/03/04/multiplexing-and-websockets/#0001-01-01`](https://mdavey.wordpress.com/2014/03/04/multiplexing-and-websockets/#0001-01-01)

## 复用与 WebSocket

关于 [C10k](http://www.kegel.com/c10k.html) 问题，WhatsApp 和其他公司多年来展示了如何提高网络服务器应用程序同时处理多个客户端的能力。High Scalability 提供了[更多](http://highscalability.com/blog/2014/2/26/the-whatsapp-architecture-facebook-bought-for-19-billion.html)的思考食物：

> 2011 年，WhatsApp 在一台机器上实现了 [100 万个建立的 TCP 会话](http://blog.whatsapp.com/index.php/2011/09/one-million/)，并且还有内存和 CPU 的剩余。2012 年，这个数字超过了 [200 万个 TCP 连接](http://blog.whatsapp.com/index.php/2012/01/1-million-is-so-2011/)。2013 年，WhatsApp [在推特上发布](https://twitter.com/WhatsApp/status/286591302185938946)：12 月 31 日，我们创下新纪录：70 亿条入站消息，110 亿条出站消息 = 一天处理总计 180 亿条消息！

在历史上，对于最后 mile 消息传递（COMET/[WebSocket](http://chimera.labs.oreilly.com/books/1230000000545/ch17.html)/等），浏览器应用程序只向流式网络应用服务器回传一个连接，并利用[消息复用](http://chimera.labs.oreilly.com/books/1230000000545/ch17.html#_binary_framing_layer_2)功能，在浏览器的应用程序视图中使用客户端功能。然而，随着服务器端可伸缩性的提高，这是否还是正确的做法？

有趣的是，SockJS 在 RabbitMQ 上[讨论](https://www.rabbitmq.com/blog/2012/02/23/how-to-compose-apps-using-websockets/)了这一点，但受到了 SockJS 问题的影响：

> 在理论上，你可以打开多个 [WebSocket](http://blog.arungupta.me/2014/02/rest-vs-websocket-comparison-benchmarks/) 连接，每个模块一个。尽管这不是最优解（因为需要处理多个 TCP/IP 连接），但这种方法适用于原生的 WebSocket。但是，不幸的是，由于 HTTP 的一个技术限制，它不适用于 SockJS，因为对于某些回退传输，不可能同时向单个服务器打开多个连接。

然而，在客户端强制进行复用之路的另一个问题是 – 浏览器最大[连接数](http://docs.pushtechnology.com/docs/4.6.0/manual/html/clients/support/c_matrixSupportBrowser.html)。不过，子域名可以解决这个问题。

GitHub 提供了一个 SockJS [复用器](http://prezi.com/luc9sbry_xf5/multiplexing-in-websockets/) – [WebSocket-multiplex](https://github.com/sockjs/websocket-multiplex)

~ mdavey 于 2014 年 3 月 4 日。

发布于[编程语言](https://mdavey.wordpress.com/category/languages/)
