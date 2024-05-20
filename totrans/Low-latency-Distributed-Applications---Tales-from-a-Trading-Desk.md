<!--yml
category: 未分类
date: 2024-05-18 05:41:54
-->

# Low-latency Distributed Applications | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2015/06/09/low-latency-distributed-applications/#0001-01-01](https://mdavey.wordpress.com/2015/06/09/low-latency-distributed-applications/#0001-01-01)

## Low-latency Distributed Applications

Andrew Brook’s [article](http://queue.acm.org/detail.cfm?id=2770868), “Evolution and Practice: Low-latency Distributed Applications in Finance” offers a good read on low latency in finance.  RFQ’s and RFS are appropriately covered coupled with the often overlooked “[Clock](https://queue.acm.org/detail.cfm?id=2745385) synchronization” 🙂  More thread than cores is also discussed – context switch.

Hopefully these types of articles will aid in educating people on the decision made during the design of low latency architectures prior to them being implemented, and deployed into production, with sometimes unfortunate results.

Its also worth calling out [Aeron’s](https://github.com/real-logic/Aeron) [Design](https://github.com/real-logic/Aeron/wiki/Design-Principles) Principles:

> To achieve low-latency with minimal variance, while achieving high throughput, it is important to define a set of design principles that guide the development. When a trade off is required then the design principles help guide the decision in choosing between competing alternatives.

There is no [free](http://www.infoq.com/presentations/java8-performance) lunch.  Performance comes at a cost – $ and/or time to develop.

~ by mdavey on June 9, 2015.

Posted in [Languages](https://mdavey.wordpress.com/category/languages/), [Trading](https://mdavey.wordpress.com/category/trading/)