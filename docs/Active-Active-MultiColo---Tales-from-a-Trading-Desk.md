<!--yml

类别：未分类

日期：2024 年 5 月 18 日 05:37:02

-->

# 主/备份多数据中心|交易台的故事

> 来源：[`mdavey.wordpress.com/2015/12/15/activeactive-multicolo/#0001-01-01`](https://mdavey.wordpress.com/2015/12/15/activeactive-multicolo/#0001-01-01)

## 主/备份多数据中心

来自领英内容工程部负责人 Erran Berger 的精彩[演示](http://www.infoq.com/presentations/linkedin-scalability-arch)。讨论集中在流处理、个人数据以及缓存失效和复制冲突。主要观点有：

+   Kafka – 数据被复制（最好和最坏的功能，因为它会导致消息的重处理）

    +   Kafka 和数据库复制结果并不是领英的解决方案——因为重复。

    +   解决方案是在用户所在的数据中心通过粘性路由服务处理用户通知。每个数据中心都有一个队列来将消息路由到其他数据中心。

    +   只处理 Kafka 消息一次，否则你会走上一条痛苦之路🙂

+   数据

    +   仅根据需要复制数据。在领英，个人数据不需要存放在所有地方。个人资料数据确实存放在各处。

    +   路由器服务决定在哪个数据中心访问哪个数据库，使用 URN 作为路由载荷，并在数据库中保存一个目录以将个人数据请求路由到正确的数据库以检索邮箱。

    +   数据中心连接需要低延迟来帮助这个解决方案

    +   数据库分片（千兆字节）达到 95TB🙂

+   缓存失效器

    +   在 LinkedIn 的情况下，缓存失效器监听数据库写入来使缓存失效，利用跨数据中心的数据库[复制](https://engineering.linkedin.com/data-replication/open-sourcing-databus-linkedins-low-latency-change-data-capture-system)

+   冲突

    +   软删除

    +   如果无法在数据模型/参与者中解决冲突，则进行自定义冲突解决。

～ 由 mdavey 于 2015 年 12 月 15 日。

发布在[数据](https://mdavey.wordpress.com/category/data/)中
