<!--yml

分类：未分类

日期：2024-05-18 06:11:55

-->

# 关于 Windows Server AppFabric、Windows Cluster 和部署的思考 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2009/11/24/thoughts-on-windows-server-appfabric-windows-cluster-and-deployment/#0001-01-01`](https://mdavey.wordpress.com/2009/11/24/thoughts-on-windows-server-appfabric-windows-cluster-and-deployment/#0001-01-01)

## 关于 Windows Server AppFabric、Windows Cluster 和部署的思考

所以我看了一些 PDC 2009 的视频。[Muralidhar 的](http://microsoftpdc.com/Sessions/FT26)“Windows Server AppFabric 缓存”演讲启发我们，通知机制现在有了批量处理功能，这主要是因为 XBox Live 每秒要处理 150 万条通知。听起来事务支持即将加入到[Velocity](http://www.microsoft.com/presspass/features/2009/nov09/11-17pdcappfabric.mspx)中——我猜这将会利用[STM.NET](http://msdn.microsoft.com/en-us/devlabs/ee334183.aspx)。应用程序[轮询](http://microsoftpdc.com/Sessions/FT26)缓存以获取通知，这让我们怀疑通知机制的实时性有多强？

从应用托管的角度来看，微软当前的路线图似乎是由 IIS 驱动的——Windows Server AppFabric 是一组集成的技术，使得构建、扩展和管理运行在[IIS](http://msdn.microsoft.com/en-us/windowsserver/ee695849.aspx)上的 Web 和组合应用程序变得更加容易。不幸的是，金融领域的卖方世界并非一切都通过 IIS 驱动——实际上，非常少的一部分。如果你看看卖方 Linux 世界，Java 进程在[VCS](http://en.wikipedia.org/wiki/Veritas_Cluster_Server) [集群](http://www.symantec.com/business/cluster-server)上运行是相当普遍的——这些进程可能正在监听消息总线，计算并将新的希腊字母或其他价格推送到另一个总线。看看微软的对应产品，[Windows Cluster](http://msdn.microsoft.com/en-us/library/aa373130(VS.85).aspx)，很明显 AppFabric 是微软的关注焦点，而 Windows Cluster ([MSCS](http://msdn.microsoft.com/en-us/library/ms952401.aspx))是遗留技术——只需看看.NET 支持（你有[通用服务](http://blogs.msdn.com/clustering/archive/2009/06/09/9712609.aspx)支持，但对于[故障转移集群 API](http://msdn.microsoft.com/en-us/library/cc296100%28VS.85%29.aspx)看起来是 C++）和 Windows Cluster 在 PDC 2009 上没有任何会议。

我对整个部署[问题](http://social.technet.microsoft.com/Forums/en-US/windowsserver2008r2highavailability/thread/b531dfdb-3000-451a-9d30-59d8da8561bf/)是不是有什么误解？

~ mdavey 于 2009 年 11 月 24 日。

发布在[未分类](https://mdavey.wordpress.com/category/uncategorized/)

标签：[微软](https://mdavey.wordpress.com/tag/microsoft/)
