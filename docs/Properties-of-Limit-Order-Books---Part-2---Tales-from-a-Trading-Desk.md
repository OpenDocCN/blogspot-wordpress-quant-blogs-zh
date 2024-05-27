<!--yml

分类：未分类

日期：2024-05-18 06:35:53

-->

# [限价订单簿的属性（第二部分）](https://mdavey.wordpress.com/2012/08/23/properties-of-limit-order-books-part-2/) - Tales from a Trading Desk

> 来源：[`mdavey.wordpress.com/2012/08/23/properties-of-limit-order-books-part-2/#0001-01-01`](https://mdavey.wordpress.com/2012/08/23/properties-of-limit-order-books-part-2/#0001-01-01)

## 限价订单簿的属性（第二部分）

订单簿的一个问题实际上是通过它们来理解延迟。TS-Associates 最近[收购](http://www.ts-a.com/News/ts-associates-acquires-correlix.html)了 Correlix。任何阅读这笔收购的新闻发布会的人都会看到关于 TS-Associates 产品套件的提及，包括 Application Tap：

> The Application Tap enables hardware assisted software instrumentation and precise time stamping

So back to the order book.  TS-Associates’s Application [Tap](http://www.ts-a.com/Application-Tap/application-tap.html) would possibly be a nice way to capture the latency of the order book, leveraging the [Java](http://www.ts-a.com/Application-Tap/technical-specs.html) API:

> The Application Tap solves the challenge of minimally invasive software instrumentation by providing a user mode API that enables software events within applications to be instrumented with minimal overhead. The Application Tap API is integrated with custom developed firmware running on a state of the art FPGA co-processor using OS kernel by-pass techniques. Instrumentation code added to applications is able to pass instrumentation metadata to the Application Tap which time stamps events to 10ns resolution, and forwards the instrumentation metadata to an external monitoring appliance, such as TipOff^®, using an on-board gigabit network interface.

~ by mdavey on August 23, 2012.

发表于[交易](https://mdavey.wordpress.com/category/trading/)

Tags: [OrderBook](https://mdavey.wordpress.com/tag/orderbook/)
