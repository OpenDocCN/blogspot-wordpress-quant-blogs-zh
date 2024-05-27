<!--yml

类别：未分类

日期：2024-05-18 06:12:41

-->

# 关于 AppFabric Beta 2 和缓存通知的说明 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2010/03/03/notes-on-appfabric-beta-2-and-cache-notifications/#0001-01-01`](https://mdavey.wordpress.com/2010/03/03/notes-on-appfabric-beta-2-and-cache-notifications/#0001-01-01)

## 关于 AppFabric Beta 2 和缓存通知的说明

在成功安装[AppFabric](http://msdn.microsoft.com/en-us/data/cc655792.aspx) beta 2 之后，我认为是时候看看如何将 Velocity 集成到一个我正在工作的概念验证（POC）中。在 CTP1/2 阶段玩过[Velocity](http://blogs.msdn.com/velocity)之后，要记住如何让缓存运行起来是非常痛苦的。因此，这里有一些说明：

+   从 Windows 7 的启动菜单中打开“Windows PowerShell 模块”

+   [Use-CacheCluster](http://msdn.microsoft.com/en-us/library/ee767586(WS.10).aspx)将提供您刚刚显示的集群视图。集群可能处于 DOWN 状态。

+   使用 Start-CacheCluster 启动集群

+   从[这里](http://www.microsoft.com/downloads/details.aspx?displaylang=en&FamilyID=55a4dceb-a116-4135-b629-035e91390031)下载 Beta 2 样本

+   值得一读的是关于集群管理的这篇文章[这里](http://blogs.msdn.com/velocity/archive/2009/03/02/how-to-use-c-to-perform-cluster-administration-in-velocity.aspx)

+   一些微软的[性能](http://blogs.msdn.com/velocity/archive/2009/04/21/more-performance-numbers.aspx)数据在这里

我现在的问题是，我已经为通知配置了 DataCacheFactoryProperties：

```

NotificationProperties = new DataCacheNotificationProperties(100, TimeSpan.FromSeconds(1));

```

但是我更新缓存时仍然得到一个异常（System.NotSupportedException：不支持通知，因为缓存没有配置为支持通知）？有人知道我错过了什么吗？答案似乎在这里[这里](http://blogs.microsoft.co.il/blogs/gilf/archive/2009/11/13/using-velocity-cache-notifications.aspx)。

**更新**：关于上述问题的答案可以在这里找到[链接](http://blogs.microsoft.co.il/blogs/gilf/archive/2009/11/13/using-velocity-cache-notifications.aspx)。如果你使用默认设置，你需要运行以下命令：

+   停止缓存集群

+   设置缓存集群 -CacheName default -NotificationsEnabled True

+   开始缓存集群

~ mdavey 于 2010 年 3 月 3 日

发布在[未分类](https://mdavey.wordpress.com/category/uncategorized/)

标签：[微软](https://mdavey.wordpress.com/tag/microsoft/)
