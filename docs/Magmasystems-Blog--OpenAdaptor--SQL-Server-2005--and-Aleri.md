<!--yml

分类：未分类

日期：2024-05-18 05:05:43

-->

# Magmasystems 博客：OpenAdaptor、SQL Server 2005 和 Aleri

> 来源：[`magmasystems.blogspot.com/2007/12/openadaptor-sql-server-2005-and-aleri.html#0001-01-01`](http://magmasystems.blogspot.com/2007/12/openadaptor-sql-server-2005-and-aleri.html#0001-01-01)

此帖子是为了任何尝试连接到命名 SS2005 实例的 Aleri 或 OpenAdaptor 用户而发布的。

我安装了多个 SQL Server 2005 的“实例”。根据

**http://msdn2.microsoft.com/en-us/library/ms378428.aspx**

，这个 JDBC 连接字符串应该能工作：

jdbc:sqlserver://MAGMALAPTOP\RPT;数据库名称=MyDatabase;集成安全=真;

在微软的

**JDBC 驱动程序 1.2 用于 SQL Server 2005**

，有一个名为 connectURL 的 Java 示例应用程序。使用上述连接字符串，这个示例应用程序运行良好，并能连接到我的 SS2005 数据库的 RPT 实例。

然而，我无法得到

**OpenAdaptor**

这个连接字符串工作。如果你想知道我为什

**Aleri**

用于其适配器的外部数据源。

在本周末花了数小时尝试使用上述连接字符串让 Aleri 连接到 SQL Server 后，我终于找到了连接字符串的一个替代语法。

新的连接字符串是：

jdbc:sqlserver://MAGMALAPTOP;实例名称=RPT;数据库名称=MyDatabase;集成安全=真;

注意那个

*实例名称*

是用一个单独的参数指定的。

所以，OpenAdaptor 可能存在问题。或者，我还有一个理论是连接字符串中的反斜杠字符被认为是一个转义字符。

©2007 Marc Adler - 保留所有权利
