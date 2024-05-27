<!--yml

类别：未分类

日期：2024-05-18 05:53:42

→

# 日志产生数据 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2014/03/04/logging-yields-data/#0001-01-01`](https://mdavey.wordpress.com/2014/03/04/logging-yields-data/#0001-01-01)

## 日志产生数据

日志可以提供关于应用程序操作活动的宝贵见解。显然，日志消息越一致，挖掘数据就越容易——想想 Splunk 等工具。相关内容：

+   [logstash](http://logstash.net/) 是一个用于管理和处理事件和日志的工具。你可以用它来收集日志、解析日志，并将其存储起来以供以后使用（例如，用于搜索）。说到搜索，logstash 带有网页界面，可以用于搜索和深入查看你的所有日志。

+   [Graylog2](http://graylog2.org/) 是一个经过现场测试的开源数据分析系统，在全球范围内被广泛使用和信赖。搜索你的日志、创建图表、发送报告，并在有事发生时收到警报。所有这些都在你的数据中心现有的 JVM 上运行。

+   [Hystrix](https://github.com/Netflix/Hystrix) 是一个用于隔离访问远程系统、服务和第三方库的延迟和容错库，旨在阻止级联失败并使复杂分布式系统中的恢复力成为可能，因为在这种系统中失败是不可避免的。

~ mdavey 于 2014 年 3 月 4 日。

发布于 [未分类](https://mdavey.wordpress.com/category/uncategorized/)
