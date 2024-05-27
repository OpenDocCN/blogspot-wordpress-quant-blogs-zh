<!--yml

category: 未分类

date: 2024-05-12 19:29:10

-->

# Tornado add_callback 考虑有害 | 编码市场

> 来源：[`etrading.wordpress.com/2018/07/16/tornado-add_callback-considered-harmful/#0001-01-01`](https://etrading.wordpress.com/2018/07/16/tornado-add_callback-considered-harmful/#0001-01-01)

## Tornado add_callback 考虑有害

### 2018 年 7 月 16 日

上周我遇到了一个有趣的问题，所以我想我应该写一篇关于这个问题博客。在工作中，我正在构建一系列基于 Tornado Python 的微服务，以实现 FX 期权预订堆栈。与其他系统通信的消息传输是 IBM MQ 系列和 AMPS 用于发布/订阅消息。自然而然，我们使用 pymqi，这是 MQ 系列传统阻塞

C API。阻塞式 API 与 Tornado 事件循环配合不佳。在传统的单线程异步风格中，Tornado 回调应该快速完成，且不应该占用线程，以便可以处理新的传入套接字事件。因此，MQ 的 PUT 和 GET 操作在另一个线程中进行，该线程使用 ioloop.add_callback()

将工作返回主线程。对于高容量队列，这意味着有很多 add_callback()调用。这就是陷阱：[Tornado 的主事件循环](http://www.tornadoweb.org/en/stable/_modules/tornado/ioloop.html#IOLoop.start)在查找新的套接字事件并将其分派给它们的处理程序之前，调度挂起的时间 outs 和回调。如果您有很多昂贵的挂起回调，那么您的代码可能会变慢，无法及时处理新的套接字事件。而这些套接字事件可能来自您的 Marathon 平台上的 HTTP GET /health 击打，那么

Marathon 会认为您的进程已死，并将其弹跳。在高流量时，这正是您不希望看到的！在这种情况下，修复方法是使 MQ 线程更加选择性地将哪些传入消息传递给其他线程，以使用 add_callback()。
