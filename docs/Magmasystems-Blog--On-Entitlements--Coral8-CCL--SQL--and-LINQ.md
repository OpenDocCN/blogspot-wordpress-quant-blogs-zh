<!--yml

分类：未分类

日期：2024-05-18 05:02:28

-->

# Magmasystems Blog: 关于权益、Coral8 CCL、SQL 和 LINQ

> 来源：[`magmasystems.blogspot.com/2008/05/on-entitlements-coral8-ccl-sql-and-linq.html#0001-01-01`](http://magmasystems.blogspot.com/2008/05/on-entitlements-coral8-ccl-sql-and-linq.html#0001-01-01)

孩子稍微大一点的好处之一就是，它让我在看洋基队比赛的时候，有时间为我的笔记本电脑做些琐事。我现在不在 Coral8 进行日常开发，因为这方面的工作已经交给了 HH。然而，我想看看我们的系统的权益处理是否可以在 Coral8 中完成，这在逻辑上是有意义的。

简要回顾：我们的 CEP 系统取出一系列原子事件，将它们送入 Coral8 处理器，产生派生事件。然而，我们不希望每个人都看到这些派生事件。我们可能在派生事件中有某些交易员不应该看到的信息，或者我们可能有关于某个金融部门的某些信息，应该隐藏在某交易台不负责该部门的人面前。

此外，我们有各种通知机制（图形用户界面、消息总线、电子邮件、聊天、短信等），应根据事件严重程度使用。我们不希望对于信息事件向交易员发送数百封电子邮件。然而，如果我们有一个“红色警报”类型的事件，我们可能会想通过电子邮件和短信通知交易员。

所以，我们将转向一个熟悉的模式，称为

**收件人列表**

. 这是书中一个有详细文档的模式

**[企业集成模式](http://www.eaipatterns.com/)**

我收到很多邮件，询问我如何成为一名交易系统开发人员。我的建议是，跑过去，而不是慢慢走，去这个网站和预订这本书。对于有经验的交易系统开发人员来说，这些东西大多是陈词滥调，但用例（尤其是乔纳森·西蒙的一个案例）物超所值。

我们已经制定了一个关于权益信息的架构和数据库，该架构和数据库将我们的用户/组列表、严重程度级别、通知机制和派生事件相结合。每当我们的 CEP 系统生成一个派生事件，我们都希望将其送入“权益加工厂”，得出一个收件人列表，以确定谁可以看到消息中的哪些信息，以及他们希望如何得知事件的发生。

这似乎是一个完美的任务，适合用 CEP 引擎。它可能只是一个额外的“丰富过滤器”，其输入连接到派生事件流的输出。这个丰富过滤器的输出包括（可能修改后的）派生事件和收件人列表。

作为一个初步步骤，我们实现了收件人列表生成器作为一个 SQL 查询使用 SQL Server 2005。这是一个由 2 个内连接和 2 个外连接组成的单条查询。它工作得相当好。

当我昨天看洋基队比赛时，我尝试将这个查询移植到 Coral8 中。我无法让这个查询的任何变体正确编译，当我试图将查询分解为 4 个流时，得到的结果与 SQL Server 完全不同。理想的“流式 SQL”语言应该是 SQL92 的超集。所以，在 Coral8 中，如果我每个 SQL Server 表都映射为一个带有“KEEP ALL”属性的 Coral8 窗口，那么我应该能够直接使用我的 SQL 查询。我想做这样的事情：

INSERT INTO RecipientListOutputStream

SELECT *[我的原始 SQL 查询]*

我给 Coral8 的团队布置了家庭作业，让他们尝试使用我的查询和模式让它在 Coral8 中运行。

所以，在花了两个小时试图解读 Coral8 的参考文档和编译器后，我决定采取另一种策略。出于好玩的心态，我决定尝试用 LINQ 来写我的 SQL 查询。我从

[`code.msdn.microsoft.com/vlinq`](http://code.msdn.microsoft.com/vlinq)

我创建了一个新的 Visual Studio 项目，将 LINQ 数据源指向权益数据库，并开始在 VLINQ 上努力工作。大约十分钟后，我写出了一个完整的 LINQ 查询，实现了我的 SQL Server 查询。

（注：在我的笔记本上，VLINQ 相当慢，我很快就放弃它了，更愿意自己用 LINQ 写查询。然而，Coral8 和其他 CEP 供应商应该把它看作是视觉代码生成器的原型。）

LINQ 有很多优点。LINQ 无处不在，而且所有种类的 LINQ 都在开发中。我很容易想象微软正在研究能够处理流数据的 LINQ 版本。现在，我认为将 LINQ 查询连接到处理流数据的水管上会相当简单。增加流式 SQL 构造是完全可以做到的。

如果微软发布了一个作为.NET 一部分的 Streaming LINQ，这将如何影响 CEP（复杂事件处理）的世界？可能的直接受害者可能是 NEsper，但没关系，因为 NEsper 现在只是 Aaron 的业余项目。然而，从长远来看，我认为 WCF（Windows Communication Foundation）、Streaming LINQ 以及一个更加针对实时流分析的 Microsoft Analysis Services 的组合将对 CEP 行业的其他部分产生巨大影响。（当然，技术是一回事。让那些 Java 和 Linux 的顽固派转投.NET 是另一回事。）

©2008 Marc Adler - 保留所有权利
