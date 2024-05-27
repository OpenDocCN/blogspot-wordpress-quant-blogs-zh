<!--yml

分类：未分类

日期：2024-05-18 05:01:49

-->

# Magmasystems Blog: Microsoft Velocity

> 来源：[`magmasystems.blogspot.com/2008/06/microsoft-velocity.html#0001-01-01`](http://magmasystems.blogspot.com/2008/06/microsoft-velocity.html#0001-01-01)

我多次在博客中提到分布式对象缓存。几乎所有大型金融机构都有在对象缓存产品上的投资。三大巨头是 Gemfire、Tangasol Coherence（现在属于甲骨文）和 GigaSpaces，传统上，这些公司一直针对 Java 和 C++市场。

曾经有过像 NCache 和 memcache 这样的利基产品，但我没有看到华尔街有很多人在使用这些产品。

如果你有段时间阅读这个博客了，你知道我一直抱怨微软没有我所说的“华尔街栈”（The Wall Street Stack）。

然而，上周，微软双脚重重地踏上了华尔街栈（Wall Street Stack）的土地，推出了 Velocity，这是他们首次尝试的分布式对象缓存。Velocity 与其他微软正在努力的一些工作（我对这些工作守口如瓶）一起，消除了我对微软忽视对华尔街重要的企业技术，特别是交易系统的领域的看法。

我不会深入我的分布式对象缓存的想法，因为我已经多次在博客中提到它们。但是，我想列出一两个我在阅读 Velocity 公告时浮现在脑海中的事情。本周我有一个与 Velocity 团队的电话会议，我希望问他们这些问题：

1) 它将保持免费吗？我希望如此。对于那些向 Gemstone、Tangasol 和 GigaSpaces 支付大量金钱的公司来说，从一个主要供应商进入这个领域的机会肯定会让其他供应商考虑降低他们的价格。在经济形势不明朗的当下，金融机构当然会欢迎不花太多钱就能拥抱这项技术的机会。

2) 它将得到支持吗？如果是，多久，由哪个产品组负责？微软以推出让他们任其衰败或过时的技术而闻名。目前，似乎微软有一个小组在从事 Velocity 工作。微软是否有意愿建立一个支持组织以妥善支持该产品？

3) 与其他微软技术之间的协同效应是什么？LINQ？SQL Server？Gemfire 有一个 SQL 查询语言，你可以将其应用于他们缓存中的数据。

4) Velocity 团队已经表示他们目前还没有推送通知。但是，当他们推出时，我们能否将其与流式 LINQ（CLINQ？）的一个版本集成？推送通知是 Velocity 目前缺失的一个极其重要的功能，但似乎很多人已经告诉 Velocity 团队这是一个主要的缺陷。

5) 支持不同的消息系统。一旦我们能够从 Velocity 获得推送通知，我们能否使用 JMS/Tibco EMS 或 RV？

6) 与网格系统的接口。 Wall Street 上最普遍使用对象缓存的方式是与网格计算结合使用。 Velocity 将如何与计算集群接口？那么 Digipede（如果我知道 John Powers，他可能已经为 Velocity 提供支持了）呢？

7) 与非 .NET 基础系统的互操作性？

8) 他们支持哪些外部数据库系统？会支持 Oracle 和 Sybase 吗？那 KDB 呢？

©2008 Marc Adler - 版权所有
