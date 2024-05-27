<!--yml

分类：未分类

日期：2024-05-18 05:25:33

-->

# Magmasystems 博客：Tibco EMS 与金融机构

> 来源：[`magmasystems.blogspot.com/2005/09/tibco-ems-and-financial-companies.html#0001-01-01`](http://magmasystems.blogspot.com/2005/09/tibco-ems-and-financial-companies.html#0001-01-01)

我负责的最后一个项目使用了 Tibco EMS 作为消息系统。我为这家主要金融机构做的这个项目已经获得了企业级许可，并且正在整个组织中部署。

Tibco 为 EMS 创建了 .NET 程序集。由于 Tibco EMS 实现了 Java 消息服务（JMS）规范，我们有一大批 .NET 开发人员将接触到 JMS。过去一直使用 MSMQ 的 Windows 程序员现在将不得不处理一个略有不同的范式。

在深入研究 JMS 之前，最好先熟悉与 JMS 相关的最佳实践和 AntiPatterns。为了帮助您，这里有一些网站：

[`www.precisejava.com/javaperf/j2ee/JMS.htm`](http://www.precisejava.com/javaperf/j2ee/JMS.htm)

(Tate 的第六章，Bitter Messages)

***Bitter Java***

AntiPatterns 书籍

[`www.manning-source.com/books/tate2/tate2_ch06.pdf`](http://www.manning-source.com/books/tate2/tate2_ch06.pdf)

进行请求/响应有点棘手。阅读这篇文章了解详情：

[`java.sys-con.com/read/49089.htm`](http://java.sys-con.com/read/49089.htm)
