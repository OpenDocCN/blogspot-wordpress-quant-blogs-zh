<!--yml
category: 未分类
date: 2024-05-18 05:53:38
-->

# Multiplexing and WebSockets | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2014/03/04/multiplexing-and-websockets/#0001-01-01](https://mdavey.wordpress.com/2014/03/04/multiplexing-and-websockets/#0001-01-01)

## Multiplexing and WebSockets

The [C10k](http://www.kegel.com/c10k.html) Problem, WhatsApp and more have over the years shown how web server application have improved to handle a high number of clients simultaneously.  High Scalability offer [further](http://highscalability.com/blog/2014/2/26/the-whatsapp-architecture-facebook-bought-for-19-billion.html) food for thought:

> In 2011 WhatsApp achieved [1 million established tcp sessions](http://blog.whatsapp.com/index.php/2011/09/one-million/) on a single machine with memory and cpu to spare. In 2012 that was pushed to over [2 million tcp connections](http://blog.whatsapp.com/index.php/2012/01/1-million-is-so-2011/). In 2013 WhatsApp [tweeted out](https://twitter.com/WhatsApp/status/286591302185938946): On Dec 31st we had a new record day: 7B msgs inbound, 11B msgs outbound = 18 billion total messages processed in one day!

Historically with last mile messaging (COMET/[WebSocket](http://chimera.labs.oreilly.com/books/1230000000545/ch17.html)/etc) connections, the browser application would only make a single connection back to the streaming web application servers, and leverage [muliplexing](http://chimera.labs.oreilly.com/books/1230000000545/ch17.html#_binary_framing_layer_2) of messages between a browsers application views using client side functionality.  However, with advance on server side scalability as above, is this still the correct approach?

Interesting, SockJS over on RabbitMQ [discusses](https://www.rabbitmq.com/blog/2012/02/23/how-to-compose-apps-using-websockets/) this very point, but is impacted by a SockJS issue:

> In theory you could open multiple [WebSocket](http://blog.arungupta.me/2014/02/rest-vs-websocket-comparison-benchmarks/) connections, one for every module. Although suboptimal (due to the need to handle multiple TCP/IP connections), this approach will work for native WebSockets. But, unfortunately it won’t for SockJS due to a technical limitation of HTTP: for some fallbacks transports it is not possible to open more than one connection at a time to a single server.

There is however another issue on the client side to force one down the multiplexing road – browser maximum [connections.](http://docs.pushtechnology.com/docs/4.6.0/manual/html/clients/support/c_matrixSupportBrowser.html) However, sub-domains could aid this

github offer a SockJS [multiplexer](http://prezi.com/luc9sbry_xf5/multiplexing-in-websockets/) – [WebSocket-multiplex](https://github.com/sockjs/websocket-multiplex)

~ by mdavey on March 4, 2014.

Posted in [Languages](https://mdavey.wordpress.com/category/languages/)