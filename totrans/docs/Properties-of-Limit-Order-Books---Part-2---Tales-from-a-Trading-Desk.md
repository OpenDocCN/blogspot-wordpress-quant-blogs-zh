<!--yml
category: 未分类
date: 2024-05-18 06:35:53
-->

# Properties of Limit Order Books – Part 2 | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2012/08/23/properties-of-limit-order-books-part-2/#0001-01-01](https://mdavey.wordpress.com/2012/08/23/properties-of-limit-order-books-part-2/#0001-01-01)

## Properties of Limit Order Books – Part 2

One of the issue with Order Books is actually getting an understanding of latency though them.  TS-Associates recently [acquired](http://www.ts-a.com/News/ts-associates-acquires-correlix.html) Correlix.  Anyone reading the press release for this acquisition would have seen references to TS-Associates product suite, including Application Tap:

> The Application Tap enables hardware assisted software instrumentation and precise time stamping

So back to the order book.  TS-Associates’s Application [Tap](http://www.ts-a.com/Application-Tap/application-tap.html) would possibly be a nice way to capture the latency of the order book, leveraging the [Java](http://www.ts-a.com/Application-Tap/technical-specs.html) API:

> The Application Tap solves the challenge of minimally invasive software instrumentation by providing a user mode API that enables software events within applications to be instrumented with minimal overhead. The Application Tap API is integrated with custom developed firmware running on a state of the art FPGA co-processor using OS kernel by-pass techniques. Instrumentation code added to applications is able to pass instrumentation metadata to the Application Tap which time stamps events to 10ns resolution, and forwards the instrumentation metadata to an external monitoring appliance, such as TipOff^®, using an on-board gigabit network interface.

~ by mdavey on August 23, 2012.

Posted in [Trading](https://mdavey.wordpress.com/category/trading/)
Tags: [OrderBook](https://mdavey.wordpress.com/tag/orderbook/)