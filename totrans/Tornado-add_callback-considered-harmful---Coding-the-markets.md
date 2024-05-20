<!--yml
category: 未分类
date: 2024-05-12 19:29:10
-->

# Tornado add_callback considered harmful | Coding the markets

> 来源：[https://etrading.wordpress.com/2018/07/16/tornado-add_callback-considered-harmful/#0001-01-01](https://etrading.wordpress.com/2018/07/16/tornado-add_callback-considered-harmful/#0001-01-01)

## Tornado add_callback considered harmful

### July 16, 2018

I ran into an interesting Tornado event loop gotcha last week, so I thought I’d blog the issue. At work I’m building a suite of Tornado Python based microservices to implement an FX options booking stack. The message transports in play for comms with other systems are IBM MQ series and AMPS for pubsub messaging. Naturally we use pymqi, which is a thin Python layer on top of MQ series traditional blocking
C API. Blocking APIs don’t play well with the Tornado event loop. In classic single threaded async style Tornado callbacks should complete quickly and not hog the thread, so that new incoming socket events can be seviced. So the MQ PUTs and GETs were in another thread, which used ioloop.add_callback( ) to
send work back to the main thread. For high volume queues, that means a lot of add_callback( ) invocations. And that’s the gotcha: [Tornado’s main event loop](http://www.tornadoweb.org/en/stable/_modules/tornado/ioloop.html#IOLoop.start) dispatches pending timeouts and callbacks before looking for new socket events and dispatching to their handlers. If you have a lot of expensive pending callbacks then your code may be slow to fall through to servicing new socket events. And if those socket events are HTTP GET /health hits from your Marathon platform, then
Marathon will conclude your process is dead and bounce it. Exactly what you don’t want when there’s high traffic! In this case the fix was to make the MQ thread more selective about which incoming messages got pitched over to the other thread with add_callback( ).