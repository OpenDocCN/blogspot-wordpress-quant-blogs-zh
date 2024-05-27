<!--yml

分类：未分类

日期：2024-05-18 05:24:37

-->

# Magmasystems Blog: NHibernate

> 来源：[`magmasystems.blogspot.com/2005/10/nhibernate.html#0001-01-01`](http://magmasystems.blogspot.com/2005/10/nhibernate.html#0001-01-01)

我正在阅读关于

[NHibernate](http://wiki.nhibernate.org/display/NH/Home)

，是一个.NET 的 O/R 映射器（它来自 Java 世界的 Hibernate）。这是其中之一

[许多](http://csharp-source.net/open-source/persistence)

适用于.NET 的 O/R 映射器。学习 NHibernate 的主要动力是 Hibernate 似乎是另一边的事实标准。由于 Finetix 是一个.NET/Java 混合公司，我想我们最终会在金融领域的项目中遇到 Hibernate。

我在过去两年的所有.NET 项目中一直使用一个自制的 O/R 层。它使用自定义属性（而不是 NHibernate 中使用的 XML 文件）在类和属性上，以生成对后端数据提供程序的调用。这些提供程序可以是 SQL Server、Oracle、ODBC、OLE DB 和 Tibco/JMS 消息。

我最后架构的项目使用了一个叫做

[Castor](http://www.castor.org/index.html)

在 WebLogic 8.1 上。有人建议我使用 Castor，因为有些人在使用 JaxB 时遇到了麻烦。而且，我很高兴地说，Castor 在这个项目中运作得非常好。

（微软的 ObjectSpaces 去哪了？）
