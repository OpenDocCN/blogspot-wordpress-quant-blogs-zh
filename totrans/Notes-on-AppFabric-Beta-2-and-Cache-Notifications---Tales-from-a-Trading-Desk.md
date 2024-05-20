<!--yml
category: 未分类
date: 2024-05-18 06:12:41
-->

# Notes on AppFabric Beta 2 and Cache Notifications | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2010/03/03/notes-on-appfabric-beta-2-and-cache-notifications/#0001-01-01](https://mdavey.wordpress.com/2010/03/03/notes-on-appfabric-beta-2-and-cache-notifications/#0001-01-01)

## Notes on AppFabric Beta 2 and Cache Notifications

After successfully installing [AppFabric](http://msdn.microsoft.com/en-us/data/cc655792.aspx) beta 2, I though it was time to look at hooking Velocity into a Proof Of Concept (POC) I’m working on. Having played around with [Velocity](http://blogs.msdn.com/velocity) during the CTP1/2 timeframe it provide painful to remember what to do to get the cache running. Hence here are a few notes:

*   Open “Windows PowerShell Modules” from the Start menu in Windows 7
*   [Use-CacheCluster](http://msdn.microsoft.com/en-us/library/ee767586(WS.10).aspx) will provide a view of the cluster you have just displayed. The cluster will probably have a status of DOWN.
*   Start the cluster using Start-CacheCluster
*   Download the Beta 2 samples from [here](http://www.microsoft.com/downloads/details.aspx?displaylang=en&FamilyID=55a4dceb-a116-4135-b629-035e91390031)
*   It’s worth reading [this](http://blogs.msdn.com/velocity/archive/2009/03/02/how-to-use-c-to-perform-cluster-administration-in-velocity.aspx) posting on cluster admin.
*   Some Microsoft [performance](http://blogs.msdn.com/velocity/archive/2009/04/21/more-performance-numbers.aspx) numbers are available here

The problem I now have is that I have configured the DataCacheFactoryProperties for notifications:

```

NotificationProperties = new DataCacheNotificationProperties(100, TimeSpan.FromSeconds(1));

```

But I still get an exception (System.NotSupportedException: Notifications are not supported because Cache is not configured to support notifications) when I update the cache? Anyone know what I’ve missed? Answer appear to be [here](http://blogs.microsoft.co.il/blogs/gilf/archive/2009/11/13/using-velocity-cache-notifications.aspx).

**Update**: There answer to the above issue as [here](http://blogs.microsoft.co.il/blogs/gilf/archive/2009/11/13/using-velocity-cache-notifications.aspx). If your running with the default settings you need to run the following:

*   Stop-CacheCluster
*   Set-CacheCluster -CacheName default -NotificationsEnabled True
*   Start-CacheCluster

~ by mdavey on March 3, 2010.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)
Tags: [Microsoft](https://mdavey.wordpress.com/tag/microsoft/)