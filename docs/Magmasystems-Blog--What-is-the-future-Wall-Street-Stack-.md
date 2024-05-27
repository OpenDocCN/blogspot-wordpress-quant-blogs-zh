<!--yml

分类：未分类

date: 2024-05-18 05:01:41

-->

# Magmasystems Blog：未来的华尔街栈是什么？

> 来源：[`magmasystems.blogspot.com/2008/06/what-is-future-wall-street-stack.html#0001-01-01`](http://magmasystems.blogspot.com/2008/06/what-is-future-wall-street-stack.html#0001-01-01)

微软最终能通过其方式开发出未来的华尔街栈吗？一系列紧密集成和支持的组件。以下是我的设想：

高速智能消息总线（与任何

Biztalk

技术）可以直接将数据转换为.NET 对象。消息总线可能有一些

SQL

内置了类似过滤功能。

总线直接将数据传递到 Velocity 对象缓存中。

Velocity 与一个

CEP

引擎。

当检测到事件时，一些 Windows

工作流

被触发并监控。

Velocity 和消息总线内置了市场数据和 FIX 消息的进程内适配器。

Velocity 可以通过

WCF

用于推送通知。

WCF

基于的服务可供应用程序和用户查询缓存的状态。

服务中介以便应用程序能够查询

关于

缓存中可用哪些数据。

一个监控堆栈可以直接从箱子中取出，用于监控整个堆栈并在检测到异常情况时发出警报。

考虑到微软当前和未来的发展方向，这个距离有多远呢？

©2008 Marc Adler - 版权所有
