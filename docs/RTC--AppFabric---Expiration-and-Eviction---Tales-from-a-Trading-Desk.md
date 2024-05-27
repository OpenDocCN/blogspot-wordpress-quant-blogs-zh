<!--yml

分类：未分类

date: 2024-05-18 06:13:15

-->

# RTC: AppFabric – 过期和驱逐 | 交易台故事

> 来源：[`mdavey.wordpress.com/2010/04/16/rtc-appfabric-expiration-and-eviction/#0001-01-01`](https://mdavey.wordpress.com/2010/04/16/rtc-appfabric-expiration-and-eviction/#0001-01-01)

## RTC: AppFabric – 过期和驱逐

实时立方体（RTC）利用[Windows AppFabric 缓存](http://msdn.microsoft.com/en-us/windowsserver/ee695849.aspx)的进展顺利。我应该在接下来的几天内有更多话要说。如果你正在使用 AppFabric，阅读“过期和驱逐”文档是值得的，否则你可能会发现你的对象消失了:-) 以下是 RTC 的默认设置：

> PS C:\Windows\system32> Get-CacheConfig
> 
> 命令 Get-CacheConfig 在命令管道中的位置 1
> 
> 为以下参数提供值：
> 
> CacheName: default
> 
> CacheName : default
> 
> TimeToLive : 10 分钟
> 
> CacheType : 分区
> 
> Secondaries : 0
> 
> IsExpirable : 是
> 
> EvictionType : LRU
> 
> NotificationsEnabled : 是

你可以很容易地看出上述问题的明显之处:-) – TTL 将导致问题

最后，有人知道 AppFabric 何时推出 RC 版吗？Beta 2 已经发布一段时间了。

~ mdavey 于 2010 年 4 月 16 日。

发布在 [未分类](https://mdavey.wordpress.com/category/uncategorized/)

标签: [微软](https://mdavey.wordpress.com/tag/microsoft/)，[实时 OLAP](https://mdavey.wordpress.com/tag/realtimeolap/)
