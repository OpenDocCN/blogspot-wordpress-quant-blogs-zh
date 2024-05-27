<!--yml

类别：未分类

日期：2024-05-18 06:20:43

-->

# Cloud Akka：微软 Azure 在哪里？| 来自交易台的故事

> 来源：[`mdavey.wordpress.com/2011/03/22/cloud-akka-where-is-microsoft-azure/#0001-01-01`](https://mdavey.wordpress.com/2011/03/22/cloud-akka-where-is-microsoft-azure/#0001-01-01)

## Cloud Akka：微软 Azure 在哪里？

在过去的一段时间里，[微软](http://msdn.microsoft.com/en-us/vstudio/gg316360)一直在开发[Visual Studio Async CTP](http://blogs.microsoft.co.il/blogs/sasha/archive/2010/10/28/visual-studio-async-ctp-the-c-perspective.aspx)，其中包括[TPL Dataflow](http://www.microsoft.com/downloads/en/details.aspx?FamilyID=d5b3e1f8-c672-48e8-baf8-94f05b431f5c&displaylang=en)：

> TPL Dataflow ([TDF](http://msdn.microsoft.com/en-us/devlabs/gg585582))是一个用于构建并发应用程序的新.NET 库。它通过用于进程内消息传递、数据流和流水线的基元来推广角色/代理导向设计。TDF 建立在.NET 4 中由任务并行库（TPL）提供的 API 和调度基础设施之上，并与 C#、Visual Basic 和 F#提供的异步语言支持集成。

我以及一些同事已经在 TPL Dataflow 之上构建了一些有趣的应用程序。但很明显，微软在支持分布式角色/代理导向应用程序的基础设施上仍然远远落后--[Cloudy Akka](http://letitcrash.posterous.com/clustered-actors-with-cloudy-akka)突显了这一点。如果你看看 Jonas 最近关于 Ping Pong 的[帖子](http://letitcrash.posterous.com/clustered-actors-with-cloudy-akka)，你会发现 Cloudy Akka 利用[Apache ZooKeeper](http://zookeeper.apache.org/)提供了一个非常有趣的可扩展解决方案，适用于交易应用程序。

在微软的世界中，我并没有看到任何有助于我将 Stat Arb ETF 代理-角色应用程序转移到[Windows Azure](http://www.microsoft.com/windowsazure/)的迹象。这是否意味着再一次在[MTS/COM+](http://en.wikipedia.org/wiki/Microsoft_Transaction_Server)时代之后，微软仍然在考虑零售消费者、客户端应用程序，而不是我们一些人必须构建的广泛企业解决方案？

~由 mdavey 于 2011 年 3 月 22 日发布。

发表在[.NET](https://mdavey.wordpress.com/category/languages/net/)、[Cloud](https://mdavey.wordpress.com/category/hpc/cloud/)

标签：[Microsoft](https://mdavey.wordpress.com/tag/microsoft/)
